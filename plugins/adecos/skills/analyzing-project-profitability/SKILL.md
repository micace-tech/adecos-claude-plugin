---
name: analyzing-project-profitability
description: Judges whether an affiliate project is making or losing money on paid traffic — EPC vs CPC, profit, break-even CPC, and a scale/hold/pause recommendation with enough data. Use when the user asks if a project is profitable, "có lãi không", whether to scale or cut budget, what CPC they can afford, or compares projects by profit or EPC.
---

# Analyzing project profitability

Reply in the user's language (Vietnamese by default). Show the formula with the numbers plugged in, so the user can check it.

## Data and role limits

- Project numbers: `adecos:get_project_report_connections(project_id, date_from, date_to)` (link refs ↔ campaigns, revenue, cost), `adecos:get_project_analytics_overview`.
- Campaign side: `adecos:get_campaign_detail`, `adecos:list_my_campaigns`.
- Team view (leaders): `adecos:get_leader_dashboard(section="financial")`.

Columns are hidden by role on the server — a hidden value comes back empty, **not zero**:
- project-staff: no clicks, cost, CPC, EPC → can judge revenue trends only.
- digital-staff: no revenue, EPC → can judge cost/CPC only.
- project-digital-staff, leader, business-leader: see both → full analysis.

If a needed value is empty, say which one and who can see it. Never estimate the missing side.

## Core math

- EPC = revenue ÷ clicks (same period, same link ref/campaign).
- Profit = revenue − cost = (EPC − CPC) × clicks.
- Break-even CPC = EPC. Bidding above EPC loses money on average.
- Use **approved** revenue when judging; pending can still be reversed. If only pending exists, discount by the program's typical reversal rate and say so.
- Match periods: affiliate dashboards and Google Ads may use different time zones and conversions lag 15–48 h — judge on days at least 2 days old (see `reconciling-affiliate-reports`).

## Recommendation

Only conclude with enough data: **≥1,000 clicks or ≥10 conversions** in the period [Industry rule of thumb]. Below that, say "chưa đủ dữ liệu" and give what is known.

| EPC : CPC | Suggest [Industry rule of thumb] |
|---|---|
| > 2.0 | scale budget +50–100%/week |
| 1.5 – 2.0 | scale +20–50% |
| 1.2 – 1.5 | optimize first (keywords, negatives, landing page) |
| 1.0 – 1.2 | hold; look for cost cuts or better commission |
| < 1.0 | pause or rebuild |

Label these as rules of thumb, not policy. Budget changes on Smart Bidding campaigns: keep each step moderate (~20%) to avoid restarting learning — see `optimizing-search-campaigns`.

## Output

Short verdict (lãi / hoà / lỗ / chưa đủ dữ liệu) → table (period, clicks, cost, revenue, EPC, CPC, profit) → one recommendation → what data is missing or uncertain.
