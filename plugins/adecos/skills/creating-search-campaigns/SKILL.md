---
name: creating-search-campaigns
description: Plans and creates a Google Ads Search campaign for an affiliate offer through adecos — checks program and policy fit, chooses bidding and match types, writes responsive search ads, looks up targeting codes, and creates the campaign paused for review. Use when the user wants to create, launch, set up or duplicate ("nhân bản") a Search campaign or "tạo chiến dịch".
---

# Creating Search campaigns

Reply in the user's language (Vietnamese by default). Tools are on server `adecos` (digital roles only — if refused, the user's role cannot create campaigns; say so).

## Before creating (checklist)

```
- [ ] Program allows paid search / Google Ads, and brand rules are known (evaluating-affiliate-programs)
- [ ] Landing page is the user's own page with real content, or direct linking is explicitly allowed
- [ ] Final URL domain = display domain; no redirect to another domain (complying-with-google-ads-policy)
- [ ] Ad account chosen: adecos:list_my_accounts → account_id
```

If any box is unknown, ask — do not create.

## Settings

- **Bidding.** New campaign without conversion data → `MAXIMIZE_CLICKS` (Google: useful for new campaigns lacking conversion data) or `MANUAL_CPC` with `manual_cpc_bid` when the user knows profitable CPCs. `MAXIMIZE_CONVERSIONS` only if conversion tracking already works.
- **Match type — always set it explicitly**; the tool defaults to BROAD. Broad match should be paired with Smart Bidding [Google]. With `MAXIMIZE_CLICKS`/`MANUAL_CPC` use `PHRASE` or `EXACT` [Industry].
- **Keywords.** Intent-led ("best X", "X review", "X price"). Respect brand rules: if brand bidding is forbidden, no brand terms in keywords or ad text.
- **Budget.** A day can spend up to 2× the daily budget; the month is capped at 30.4× [Google]. Size the daily budget so 2× is still acceptable.
- **Targeting.** `adecos:search_ad_locations` / `adecos:search_ad_languages` return Google codes → `location_codes`, `language_codes`. Leave empty only for intentional worldwide targeting.
- **Ads (RSA).** Minimum 3 headlines + 2 descriptions; aim for up to 15 headlines (≤30 chars) and 4 descriptions (≤90 chars) [Google]. Include the main keyword in some headlines; vary angles (benefit, proof, CTA). No unverifiable claims ("#1", "official site") — especially not "official" for a brand you are only an affiliate of.

## Create

Show the full plan (account, name, URL, budget, bidding, match type, keywords, locations, languages, headlines, descriptions) and ask for confirmation. Then `adecos:create_campaign(...)`. Campaigns are **always created paused**; names must be unique per account.

After creation tell the user: review it in Google Ads, then enable it with `adecos:set_campaign_status(ENABLED)` or in Google Ads. Suggest an alert: `adecos:list_alert_options` → `create_campaign_alert` (budget, CPC or click thresholds).

## Duplicating

`adecos:duplicate_campaign(campaign_id, target_account_id, new_campaign_name, daily_budget)` → returns a job; poll `adecos:get_duplicate_job`. The copy is created paused. Same policy checklist applies to the target account.
