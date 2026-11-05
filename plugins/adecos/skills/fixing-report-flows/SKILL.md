---
name: fixing-report-flows
description: Repairs a broken report flow when an affiliate dashboard changed its layout — observes the page, clicks through to the right report and date filter, verifies the numbers, and saves the new path as a new flow version. Use when run_saved_flow fails, a flow is "flow_broken", the partner site "đổi giao diện", or the user wants to teach or re-teach how to reach a report.
---

# Fixing report flows

Reply in the user's language (Vietnamese by default).

Needs `adecos-local` (Claude Desktop/Code on the machine with the adecos app open). Without it, say so and stop.

## Loop

1. Start clean: `adecos-local:act(action="navigate", url=<report page>)`. Navigating also starts a new recording — only steps after the latest navigate are saved. Get the URL from the failed flow (`adecos:get_report_flow` shows its steps) or ask the user.
2. `adecos-local:observe_page` → look at the screenshot and the numbered elements.
3. One `adecos-local:act` per step (`click` by `index`; `select`/`fill` only if unavoidable).
4. Observe again after every act — indexes are only valid for the latest observation.
5. Stop when the table shows the target date (usually a "Yesterday"/"Hôm qua" preset). Max ~10 acts; if still stuck, describe what you see and ask the user.
6. Verify: `adecos-local:read_report`. Do not save a flow whose reading is `warn` on the date check.
7. Ask the user, then `adecos-local:save_flow_from_session(note=<what changed>)`. It becomes the project's current flow; older versions stay restorable (`adecos:list_report_flow_versions`, `adecos:restore_report_flow`).

## What can be saved

Only paths made of **navigate (URL without a fixed date) + clicks** can be saved, because replay repeats values literally — a typed date or a dated URL would replay yesterday's date forever. Prefer preset buttons ("Yesterday", "Hôm qua", "Last 1 day") over typing dates. If the only way is typing a date, collect today's numbers anyway and tell the user the flow cannot be saved; the app's AI handles it daily.

## Never

- Type into password or one-time-code fields (the tool refuses). If you hit a login page, ask the user to log in in the open window.
- Click "Delete", "Remove", "Cancel subscription", payment or settings-changing buttons on partner sites. Reading reports only.
- Save a flow you did not verify with `read_report`.
