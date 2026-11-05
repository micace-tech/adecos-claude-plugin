---
name: optimizing-search-campaigns
description: Reviews and optimizes running Google Ads Search campaigns for affiliate offers — when to wait, which keywords and ads to pause, adding keywords, bidding and budget changes — using Google's guidance and labeled rules of thumb. Use when the user asks to optimize, improve, cut waste, review keywords or ads, change bidding/target CPA/ROAS or budget, or asks why a campaign underperforms.
---

# Optimizing Search campaigns

Reply in the user's language (Vietnamese by default). Tools on server `adecos` (digital roles). Numbers that change over time are in [reference/google-ads-numbers.md](reference/google-ads-numbers.md).

## First: should we touch it at all?

- Status **Learning** → don't change anything; if changes are unavoidable, make them all at once [Google]. Learning restarts after new/changed bid strategy, settings, or adding/removing campaigns, ad groups, keywords [Google].
- New ads need up to 24 h of review before judging.
- Judge Smart Bidding over enough time (see reference file); don't react to one bad day.

## Review order

1. `get_campaign_detail(campaign_id, date_from, date_to)` — spend, clicks, conversions, CPC. Pair with revenue via `analyzing-project-profitability` if the role can see it.
2. `list_campaign_keywords(campaign_id, search?)` — per-keyword clicks/cost/conversions (null = not synced yet, not zero).
3. `list_campaign_ads(campaign_id)` — per-ad performance.

## Keyword decisions

- **Pause** (`set_keyword_status(..., "PAUSED")`) a keyword that spent **2–3× the target CPA (or the commission per conversion) with no conversion** and has ≥~30 clicks [Industry]. First rule out the landing page and the match type as the cause.
- **No delete via adecos**: "delete" = pause. "Edit" a keyword (text or match type cannot change in Google) = `add_campaign_keywords` with the new one + pause the old.
- **Add** with `add_campaign_keywords(campaign_id, ad_group_id, keywords, match_type)` — ad_group_id comes from `list_campaign_keywords`/`list_campaign_ads`. New keywords are live immediately.
- Negative keywords don't match close variants (negative "flowers" does not block "red flower") [Google]. Adding negatives is not available through adecos — do it in Google Ads.

## Ad decisions

Keep ≥2 RSAs per ad group [Google]. Pause clearly losing ads with `set_campaign_ad_status(..., "PAUSED")` only after they have comparable impressions to the winner. Avoid pinning unless required; if pinning, pin 2–3 assets per position [Google].

## Bidding & budget

- `update_campaign_bidding(campaign_id, strategy, target_cpa|target_roas)` — TARGET_CPA, TARGET_ROAS or MAXIMIZE_CONVERSIONS. Check conversion volume first (reference file).
- Change budgets/targets in moderate steps (~20% at a time) [Industry — Google publishes no limit].
- Since 17 Aug 2026, budget-limited tCPA/tROAS campaigns stay close to the target even when budget changes; Google won't adjust targets for you [Google].
- Network settings (`update_campaign_settings`): turning off Search Partners / Display is a common affiliate choice for control [Industry].

## Always

Explain the expected effect and the risk before any write; every write changes the real Google Ads account. Prefer one change, then wait and measure.
