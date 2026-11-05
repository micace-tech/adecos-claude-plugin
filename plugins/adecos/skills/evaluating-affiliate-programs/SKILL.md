---
name: evaluating-affiliate-programs
description: Finds and evaluates affiliate programs before buying paid traffic — shortlists from the adecos catalog by affiliate signals (opportunity score, brand search volume, brand CPC, break-even CR, who already runs ads), then checks commission, cookie, payout terms and whether Google Ads and brand bidding are allowed, and gives a Go / Test / No-go verdict. Use when the user is choosing a project, searching the project catalog ("kho Khám phá", "dự án tiềm năng", "có cửa lãi"), asks if a program is worth running ads for, or compares programs.
---

# Evaluating affiliate programs

Reply in the user's language (Vietnamese by default).

## Data (server `adecos`)

- `search_preset_projects` — catalog search, max 20 rows, each with a compact `signal` (null = not computed yet). Filters:
  - basics: `keyword`, `industry`, `niche`, `commission_type`, `source` (e.g. "PartnerBoost"), `recurring`, `status` ("ACTIVE" for running programs), `blocked_country`, `min_monthly_visits` / `max_monthly_visits`;
  - `preset`: `"potential"` or `"profitable"` — the same thresholds as the web buttons "Dự án tiềm năng" / "Có cửa lãi";
  - `ads_states`, `ranges` (e.g. `{"brandVolume": {"min": 5000}, "crBreakevenLow": {"max": 0.03}, "score": {"min": 60}}` — CR values are 0–1), `exclude_generic_name`, `exclude_brand_bid_banned`, `exclude_no_program`; explicit values override the preset;
  - `sort_by`: `opportunity_score`, `brand_volume`, `cr_breakeven_low` (lowest first), `commission_per_order`, `aov`, `monthly_visits`, `commission_max`, `cookie_days`….
- `get_explored_project_detail(project_id)` — full signal (with `score_explain`, `potential_reasons`, `commission_source`), policy, traffic, commission, cookie, payment.
- After a Go: `save_project` (bookmark into the user's projects) — ask first.

Policy fields worth reading: `commission_type` (CPS, REVSHARE, CPA, CPL, CPC, CPM, HYBRID, REFERRAL, RECURRING…), commission min/max and unit (percent vs fixed), `recurring`, `cookie_days`, payment cycle and minimum, `ads_ok`, `brand_ok`, `ad_limits`, blocked/restricted countries, monthly visits. Empty ≠ "allowed": an unknown policy is a question, not a yes.

## Shortlisting with signals

Typical asks → call:
- "dự án có cửa lãi" → `preset="profitable"`, `sort_by="opportunity_score"`.
- "chưa ai chạy quảng cáo" → `ads_states=["none","idle"]`.
- "ngách X, lượt tìm brand trên 5k" → `niche` + `ranges={"brandVolume":{"min":5000}}`.

Reading the signal (all are adecos estimates, not measured results):
- **`ads_state`** — Google ads on the brand/domain in the last 30 days: `none` nobody, `idle` ads exist but none shown in 30 days, `others` only non-brand advertisers, `brand` the brand runs its own ads (hard to win brand traffic; score −40), `unknown` not reliable (subdomain or shared platform). `ads_others_active` > 5 = crowded (score −10). Brand detection is ~5–10% wrong.
- **`brand_volume`, `brand_cpc_low/high`** — Keyword Planner, global, for the exact brand name. Worthless when `generic_name` is true (the name is a common word).
- **`commission_per_order_usd`** — estimated from network EPC/CR, store AOV × %, SaaS price × % × months, or fixed payout; check `commission_source` in the detail before trusting it.
- **`cr_breakeven_low`** = brand CPC low ÷ commission per order: the conversion rate needed to break even on brand clicks. ≤ 5% is "có cửa lãi"; e.g. 0.017 = 1 sale per ~58 clicks. Generic keywords usually cost more than the brand CPC — redo the math for them.
- **`opportunity_score`** 0–100 = size (brand searches, 40) + commission (20) + break-even room (40) − penalties. Use it to rank, not to decide; read `score_explain`.
- **`is_potential`** = brand searches ≥ 1,000, not a generic name, brand bidding not banned, a program exists, ads state not `brand`/`unknown`, CPC < $100. **`is_profitable`** = potential + break-even CR ≤ 5%.
- `brand_bidding_policy: prohibited` or `affiliate_program: not_found` → treat as hard stops below.

Show a shortlist as a table: name · score · brand searches · CPC low–high · commission/order · break-even CR · ads state · why it's interesting. Then evaluate the top picks below.

## Hard stops (No-go until clarified)

- **Paid search not allowed** (`ads_ok` false, or terms forbid PPC). Running ads against program rules is also a Google Ads policy violation ("Unfair advantage" policy) [Google] — risk to the whole ad account, not just lost commission.
- **Brand bidding**: if the terms forbid bidding on the brand (TM) or brand + words like "coupon/review" (TM+), or forbid the brand in ad text, plan keywords without the brand and add brand negatives. Breaking it typically means reversed commissions [Industry].
- **Direct linking banned** (ad click must land on your own page, not straight on the tracking link) — needs a landing page with real content; thin "bridge" pages are disapproved by Google — see `complying-with-google-ads-policy`.
- Target country in blocked countries.

## Quality signals [Industry rules of thumb]

- Cookie ≥30 days preferred; a lower rate with a long cookie can beat a higher rate with a short one.
- Reversal rate above ~10% is a warning (cuts real EPC one-for-one).
- Conversion rates far above ~10% claimed by a network deserve suspicion.
- Clear terms on payout threshold (commonly ~$50–200), hold period (commonly 30–60 days) and reversal reasons. Vague terms = risk.
- Recurring/RevShare is attractive but pays slowly — fine for profit, bad for cash flow.

## Expected economics

Start from `cr_breakeven_low` when it exists. Otherwise estimate break-even CPC = expected conversion rate × average commission (= EPC). Compare with typical CPC for the main keywords (ask a digital teammate, or use the user's existing campaigns via `analyzing-project-profitability`). If break-even CPC is clearly below likely CPC, say No-go.

## Output

Verdict **Go / Test small / No-go** → 3–5 reasons → open questions to ask the program manager (PPC allowed? brand bidding? direct linking? countries?) → if Test: suggested test budget ≈ 10× the payout per conversion before judging [Industry].
