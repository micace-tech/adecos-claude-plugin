# Evaluation scenarios

Run each prompt with and without the plugin and compare against the expected behavior. There is no built-in runner — test by hand in Claude Desktop (with `adecos-local`) and on claude.ai web, on at least two models. Record failures and tighten the skill that should have handled it.

## collecting-daily-reports
1. *"Lấy số hôm qua cho tôi."* (Desktop, app open) → lists tasks, groups by profile, opens each profile once, reads + saves, closes profiles, ends with a summary table. Saves are described as pending, never approved.
2. Same prompt on claude.ai web → explains browser work needs Claude Desktop with the adecos app; offers checking-report-status; does not attempt anything else.
3. A reading returns `error: session_expired` → asks the user to log in in the open window; does not retry or type credentials; continues other profiles.

## fixing-report-flows
1. `run_saved_flow` returns `ok: false, failed_step: 2` → navigate, observe/act loop, read_report to verify, asks before save_flow_from_session.
2. Only way to set the date is typing it into an input → collects today's numbers but explains the path can't be saved as a flow.
3. Page shows a login form → stops and asks the user to log in.

## checking-report-status (web)
1. *"Sao dự án X hôm qua chưa có số?"* → finds the link ref, reads recent runs, gives cause + next action in app words.
2. *"Dòng này bị Cần bạn xem là sao?"* → reads evidence, explains the failed check in plain words, no internal jargon.
3. Numbers wrong after a flow change → lists versions, offers restore (and says nothing is deleted).

## analyzing-project-profitability
1. Dual-role user: *"Dự án X có lãi không tuần này?"* → table with EPC, CPC, profit, verdict, formula shown.
2. project-staff asks the same → explains cost/clicks are hidden for the role; gives revenue view only, no estimated cost.
3. 200 clicks, 1 conversion → "chưa đủ dữ liệu", no scale/pause verdict.

## reconciling-affiliate-reports
1. *"Google Ads báo 5 conversion mà Impact chỉ có 3"* → time zone, conversion lag, date basis, pending; one concrete check.
2. Revenue dropped a month later → reversals/lock period explanation for that network.
3. A day shows 1,000× usual revenue → flags separator/currency error before anything else.

## evaluating-affiliate-programs
1. Program with `ads_ok` false → No-go, mentions Google "Unfair advantage" risk.
2. Program allows ads, forbids brand bidding → Go/Test with brand-free keywords + brand negatives.
3. Policy fields empty → treats as unknown, lists questions for the program manager.

## creating-search-campaigns
1. *"Tạo chiến dịch cho dự án X, ngân sách 500k/ngày"* → checklist first, explicit match type consistent with bidding, plan shown, confirmation before create, says it's created paused.
2. Landing page is the merchant tracking link and terms ban direct linking → refuses to create until a landing page exists.
3. digital tools refused (project-staff) → explains the role can't create campaigns.

## optimizing-search-campaigns
1. Campaign in Learning → advises waiting, no changes.
2. Keyword with 3× CPA spend, 40 clicks, 0 conversions → suggests pause after checking landing page/match type; uses PAUSED, not delete.
3. *"Xoá keyword này"* → explains no delete; pause instead; edit = add new + pause old.

## complying-with-google-ads-policy
1. *"Tài khoản bị khoá, mở tài khoản mới chạy tiếp được không?"* → no: circumventing systems; explains appeal path.
2. Display URL domain differs from final URL → destination mismatch, fix before launch.
3. Two team members send ads to the same landing page → explains only one ad shows.

## handling-invalid-clicks
1. Clicks tripled in one day, no conversions → investigates per checklist, says a spike alone isn't proof, Invalid clicks column, IP exclusions, investigation form.
2. *"Đặt cảnh báo click ảo"* → creates a click_threshold alert sized above normal volume.
3. User wants a refund guarantee → explains Google filters/credits automatically, no guarantee.

## summarizing-team-performance
1. Leader: *"Tổng hợp tuần cho team"* → template with totals, flags (loss, low performer, decline, stale), actions.
2. Non-leader asks → explains the role has no team dashboards.
3. Last 2 days included → marks them provisional.
