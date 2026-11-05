---
name: evaluating-affiliate-programs
description: Evaluates an affiliate program before buying paid traffic for it — commission model, cookie, payout terms, traffic, and especially whether the program allows Google Ads and brand bidding — and gives a Go / Test / No-go verdict. Use when the user is choosing a project, searching the project catalog ("kho Khám phá"), asks if a program is worth running ads for, or compares programs.
---

# Evaluating affiliate programs

Reply in the user's language (Vietnamese by default).

## Data (server `adecos`)

- `search_preset_projects(keyword, industry, niche, commission_type, blocked_country, min_monthly_visits, ...)` — catalog search.
- `get_explored_project_detail(project_id)` — policy, traffic, commission, cookie, payment.
- After a Go: `save_project` (bookmark into the user's projects) — ask first.

Catalog fields worth reading: `commission_type` (CPS, REVSHARE, CPA, CPL, CPC, CPM, HYBRID, REFERRAL, RECURRING…), commission min/max and unit (percent vs fixed), `recurring`, `cookie_days`, payment cycle and minimum, `ads_ok`, `brand_ok`, `ad_limits`, blocked/restricted countries, monthly visits. Empty ≠ "allowed": an unknown policy is a question, not a yes.

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

Estimate break-even CPC = expected conversion rate × average commission (= EPC). Compare with typical CPC for the main keywords (ask a digital teammate, or use the user's existing campaigns via `analyzing-project-profitability`). If break-even CPC is clearly below likely CPC, say No-go.

## Output

Verdict **Go / Test small / No-go** → 3–5 reasons → open questions to ask the program manager (PPC allowed? brand bidding? direct linking? countries?) → if Test: suggested test budget ≈ 10× the payout per conversion before judging [Industry].
