---
name: collecting-daily-reports
description: Collects yesterday's (or a given day's) affiliate report numbers for the link refs the user is responsible for, by driving their logged-in browser profiles through the adecos desktop app, then saving each reading for approval. Use when the user asks to get, pull, collect or "lấy số" daily report numbers, run the daily report, or fill in referrals/revenue for a date.
---

# Collecting daily reports

Reply in the user's language (Vietnamese by default). Use the app's words: "Lấy số", "Đã kiểm tra", "Cần bạn xem", "Cần đăng nhập lại", "Tự nhập".

## Requirements

Browser work needs the local server `adecos-local`, which only exists in Claude Desktop / Claude Code on the machine running the adecos app (open and signed in). If `adecos-local` tools are missing — e.g. on claude.ai web — say so, offer `checking-report-status` instead, and stop. Do not try to collect numbers another way.

If a tool is refused for permissions, the user's role does not collect reports (digital-staff). Say so; do not guess.

## Workflow

Copy and track:

```
- [ ] 1. List tasks and pick the date
- [ ] 2. Group by browser profile
- [ ] 3. For each link ref: run flow → read → confirm → save
- [ ] 4. Close profiles
- [ ] 5. Summary table
```

1. **List.** `adecos-local:list_my_report_tasks`. Default date = yesterday in Vietnam time (UTC+7). Skip rows with `auto: false` unless the user names them. Rows with no profile or `has_flow: false` cannot be collected automatically — list them at the end as "chưa gắn hồ sơ" / "chưa dạy đường đi".
2. **Group** link refs by `profile_id`: open each profile once, run all its link refs, close once. A profile with `profile_locked_elsewhere: true` is open on another machine — skip it and report it.
3. **Per link ref:**
   - `adecos-local:open_profile` (once per profile).
   - Link refs with a dated URL template need nothing extra — `read_report` opens the URL itself. Otherwise `adecos-local:run_saved_flow`. If it returns `ok: false`, switch to the `fixing-report-flows` skill for this link ref, then come back.
   - `adecos-local:read_report(profile_id, link_ref_id, metric_date)`.
   - Decide:
     - `error: session_expired` → ask the user to log in again in the open browser window; never type credentials. Continue with other profiles meanwhile.
     - `status: ok` → save without asking, unless the user asked to confirm each row.
     - `status: warn` → show the numbers plus each failed check in plain words and ask before saving. If the user corrects a number, pass only the corrected fields.
   - `adecos-local:save_report_reading`. Numbers are always saved as pending — the person in charge approves them on the web.
4. `adecos-local:close_profile` for every profile you opened, even after errors.
5. **Summary** (one table): project · link ref · referrals · revenue · status (Đã kiểm tra / Cần bạn xem / Cần đăng nhập lại / lỗi). End with what the user must do next (log in, approve "Cần bạn xem" rows on the web, teach missing flows).

## Rules

- Never claim a number is approved. Saved = waiting for approval.
- One `read_report` → at most one save. To re-read, call `read_report` again.
- Never retry `session_expired` automatically.
- Referrals are conversions, not clicks. Revenue is the affiliate's commission, not the merchant's sales.
- Manual fallback: if the user dictates a number for a day with no reading, use `adecos:save_daily_metrics` (one day, only when the day is still empty).
