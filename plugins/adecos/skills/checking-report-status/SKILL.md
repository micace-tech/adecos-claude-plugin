---
name: checking-report-status
description: Explains the state of the user's daily affiliate reports without opening any browser — which link refs have flows and profiles, recent run results and failures, and why a number is marked "Cần bạn xem" — and says what to do next. Works on claude.ai web. Use when the user asks about report status, missing numbers, failed runs, warnings, evidence screenshots, or flow versions.
---

# Checking report status

Reply in the user's language (Vietnamese by default). Read-only: this skill never collects or saves numbers.

## Tools (server `adecos`)

- `list_report_link_refs(project_id?)` — every link ref in the daily report: profile, `flow` (`recorded_steps` / `url_template` / `none`), `auto`, last status.
- `list_report_runs(project_id, link_ref_id, limit)` — recent runs, failures included.
- `get_report_evidence(project_id, link_ref_id, metric_date)` — numbers, check results, screenshot link.
- `get_report_flow`, `list_report_flow_versions`, `restore_report_flow`.

Refused for permissions → the role does not own reports (digital-staff), or the link ref belongs to someone else. Say so.

## Diagnose → next action

| What you see | Meaning | Tell the user |
|---|---|---|
| `flow: none` | Never taught | Open the app → "Lấy số" once to teach, or use `fixing-report-flows` in Claude Desktop |
| no profile | No browser profile attached | Attach one in the app ("Gắn hồ sơ") |
| run `session_expired` | Partner site logged out | Log in again in that profile, then re-run |
| run `flow_broken` | Partner page changed | `fixing-report-flows`, or let the app's AI retry |
| evidence `status: pending` | Saved, waiting for approval | Approve on the web; only the person in charge can approve |
| a check failed | "Cần bạn xem" | Explain the failed check below in plain words |

## The five checks behind "Đã kiểm tra"

All must pass; any failure → "Cần bạn xem" with a reason:

1. **Date** — the date shown on the page equals the requested day ("Yesterday" is resolved in Vietnam time).
2. **Currency** — same currency as when the flow was taught.
3. **Label** — the label taught next to the commission (e.g. "Commissions") is still on the page.
4. **Number on page** — every number read from the screenshot also appears in the page text.
5. **30-day range** — revenue per referral vs this link ref's own last 30 days (needs ≥7 days of history; flags beyond ~3 standard deviations).

Never use internal words (guardrail, anchor, selector, σ) with users.

## Fixing a bad flow version

If numbers went wrong right after a flow change, list versions and offer `restore_report_flow` to the previous one. Restoring deletes nothing.
