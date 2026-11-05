---
name: summarizing-team-performance
description: Produces a leader's daily or weekly summary of the team — revenue, cost, profit, EPC, top and weak members, loss-making projects, stale reports — from the adecos leader and department dashboards, with concrete follow-ups. Use when a leader or business-leader asks for a team/department report, "tổng hợp tuần", who is underperforming, or where the team is losing money.
---

# Summarizing team performance

Reply in the user's language (Vietnamese by default). For leaders and business-leaders only — if the tools below are refused, the user is not a leader; say so.

## Data (server `adecos`)

- `get_leader_dashboard(section, start_date, end_date)` — `overview` (KPIs + change vs previous period), `financial` (revenue, cost, profit, EPC), `operations`.
- `get_team_performance(start_date, end_date)` — per member, grouped by role.
- `get_department_overview(start_date, end_date)` — business-leader, whole department (fails if the account has no department assigned).
- Drill-down: `analyzing-project-profitability` for one project; `checking-report-status` only works for link refs the user personally owns.

## Defaults

- Weekly = last 7 full days ending yesterday; compare with the 7 days before. Daily = yesterday vs the same weekday last week.
- Leave the last 2 days out of profit conclusions or mark them provisional: affiliate numbers may still be pending and Google conversions lag up to 48 h.
- A change of −100% in the dashboards means the previous period was zero, not a real drop.

## What to flag

Mirror the department signals adecos already uses:
- **Loss projects:** profit < 0 in the period.
- **Low performers:** below 50% of the same-role median (revenue for project-staff, profit for digital-staff) — only meaningful with ≥3 people in that role.
- **Declining:** revenue or profit down more than 20% vs the previous period.
- **Stale:** link refs with no new numbers for 5+ days.

Judge people fairly: project-staff are measured on revenue, digital-staff on profit; a new project in its test phase is not a "loss" yet — see the data threshold in `analyzing-project-profitability`.

## Output template

```
## Tổng hợp <period>
**Tổng:** doanh thu … · chi phí … · lợi nhuận … · EPC … (so với kỳ trước: …)
**Điểm tốt:** 1–3 bullets
**Cần chú ý:** loss projects, low performers, declines, stale reports (each with the number)
**Việc cần làm:** 3–5 concrete actions with an owner
```

Never approve or change members' numbers on their behalf — only the person in charge approves. Keep personal comparisons factual and private to the leader.
