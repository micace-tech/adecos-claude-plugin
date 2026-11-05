---
name: handling-invalid-clicks
description: Investigates suspected click fraud and invalid traffic on Google Ads campaigns — what Google already filters and refunds, which signals matter, IP exclusions, requesting a Google investigation, and adecos click alerts. Use when clicks spike, CTR looks abnormal, many clicks bring no conversions, the user says "click ảo" / "bị click tặc", or a click-fraud alert fires.
---

# Handling invalid clicks

Reply in the user's language (Vietnamese by default). Facts are Google Help (checked 2026-10) unless marked [Industry].

## What Google already does

- Invalid clicks are filtered automatically and removed from metrics and billing; invalid clicks found after billing are credited on a later invoice. Conversions can exceed clicks when a converting click is filtered later. (google-ads/answer/42995)
- There is no industry standard for a "normal" invalid-traffic rate. Traffic spikes, zero-second visits or shared IPs are **not proof** of fraud. (answer/11182074)

## Investigate (in order)

1. Look at `adecos:get_campaign_detail` for the spike window: clicks, cost, conversions, CPC vs the previous weeks.
2. Ask the user to add the **"Invalid clicks"** column at campaign level in Google Ads to see what Google already removed.
3. Check targeting: location option set to **Presence** (people in the location), not interest; add negative keywords for irrelevant queries. (answer/11182074)
4. Compare with the affiliate dashboard: clicks with zero conversions across many days is a stronger signal than one spiky day.

## Act

- **IP exclusions:** up to 500 per campaign, wildcards like `1.2.3.*` allowed; account-level exclusions cover all campaign types. Done in Google Ads (not available through adecos). (answer/2456098)
- **Request an investigation:** Click Quality form, up to the past 60 days, with Customer ID, dates, campaigns, keywords, and server logs (IP, device, GCLID). Credits don't change historic metrics — see the Invalid Activity Credit report. (answer/11182074)
- **Contain damage meanwhile:** pause the affected keywords/ads (`set_keyword_status` / `set_campaign_ad_status`) or the campaign (`set_campaign_status`) — explain the trade-off first.
- Vendor claims about refund rates or "one request per 60 days" are unreliable [Industry]; don't quote them as fact.

## adecos alerts

`adecos:list_alert_options` → `create_campaign_alert` with `click_threshold` (daily clicks) or `cpc_threshold`; manage with `list_campaign_alerts`, `update_campaign_alert`, `set_campaign_alert_active`. The click alert compares the day's total clicks to the threshold and notifies at most once a day — set it above normal daily volume, e.g. ~1.5–2× the recent daily average [Industry].
