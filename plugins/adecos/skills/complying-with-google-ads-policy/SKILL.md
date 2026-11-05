---
name: complying-with-google-ads-policy
description: Checks affiliate Google Ads setups against the Google Ads policies that most often hit affiliates — bridge/thin pages, destination mismatch, affiliate program rules, same-landing-page limits, trademarks, circumventing systems — and guides disapproval and suspension appeals. Use before launching or editing campaigns, when an ad is disapproved, an account is suspended or warned, or the user asks whether something is allowed.
---

# Complying with Google Ads policy (affiliates)

Reply in the user's language (Vietnamese by default). All points are Google policy (checked 2026-10) unless marked [Industry]. When unsure, say "chưa chắc" and link the policy — never promise an ad will be approved.

## Pre-launch checklist

```
- [ ] Landing page has original, useful content — not a page that only sends users elsewhere
- [ ] Display URL domain = final URL domain; final URL does not redirect to another domain; tracking template leads to the same content; page is crawlable (no HTTP errors)
- [ ] Program terms allow Google Ads (and brand keywords/ad text if used)
- [ ] Not another affiliate's copy of the same landing page targeting the same queries
- [ ] Brand names in ad text only if allowed (reseller/informational exception or authorization)
- [ ] No second account to replace a suspended one
```

## The rules

- **Insufficient original content / bridge pages.** Destinations "solely designed to send users elsewhere" or copied content without added value are disapproved; Google warns ≥7 days before suspending for this. (adspolicy/answer/6368661)
- **Abusing the ad network.** Bridge/gateway pages, arbitrage (pages mainly for ads), cloaking are banned. (answer/6020954)
- **Unfair advantage.** Bans "affiliates that advertise on Google Ads against the applicable affiliate program rules" and showing more than one ad for your site in one ad location. → Breaking a program's PPC/brand rules is a Google violation too. (answer/15936768)
- **Same landing page.** Ads from different advertisers leading to the same or near-identical page can't show at once — only the highest Ad Rank shows; "particularly applicable to affiliate and reseller advertisers". (answer/146527)
- **Destination mismatch.** See checklist. (answer/6368661)
- **Trademarks.** Google does not restrict brand names as keywords; restrictions apply to ad text after the owner complains. Resellers/informational sites can use them if the page mainly sells/informs about that product. Authorization comes only from the trademark owner. Program terms may still forbid brand bidding. (answer/6118)
- **Circumventing systems — most dangerous.** Cloaking, multiple-account abuse, evading enforcement → suspension on detection without warning; reinstatement only in compelling circumstances. **Opening a new account after a suspension counts.** Linked/related accounts can be suspended too — critical for teams managing many accounts and MCCs. (answer/15938075, google-ads/answer/2375414)

## Strikes and suspensions

Repeat violations: strike 1 → 3-day hold, strike 2 → 7-day hold, strike 3 → suspension. (google-ads/answer/2375414)

## Appeals

- **Disapproved ad:** fix first, then Policy manager → "Dispute decision" or "Made changes". Wait ≥24 h between appeals of the same ads; after 3 failed appeals contact support. Decisions older than 6 months can't be appealed in-account (since 21 Jul 2026). (google-ads/answer/9338593)
- **Suspended account:** one appeal per account via Contact Us; ≥6 months to appeal; duplicate appeals may not be processed; all linked accounts must comply first. (google-ads/answer/2375414)

adecos cannot appeal for you — guide the user to Google Ads. Note: adecos has an "account suspended" alert type but it is not implemented yet; don't promise automatic suspension alerts.
