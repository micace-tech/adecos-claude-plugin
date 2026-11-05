# adecos plugin for Claude

One plugin for every adecos role. Skills teach Claude the team's workflows and expert know-how; permissions stay on the adecos servers (each role only gets its own tools and columns), so there is no need for per-role plugins.

## Contents

| Skill | For | Needs |
|---|---|---|
| collecting-daily-reports | project staff | Claude Desktop/Code + adecos app (`adecos-local`) |
| fixing-report-flows | project staff | `adecos-local` |
| checking-report-status | project staff | `adecos` (works on web) |
| evaluating-affiliate-programs | project staff | `adecos` |
| analyzing-project-profitability | everyone (full view: dual role, leaders) | `adecos` |
| reconciling-affiliate-reports | everyone | — |
| creating-search-campaigns | digital staff | `adecos` |
| optimizing-search-campaigns | digital staff | `adecos` |
| complying-with-google-ads-policy | digital staff | — |
| handling-invalid-clicks | digital staff | `adecos` |
| summarizing-team-performance | leaders | `adecos` |

Skills are written in English; Claude answers in the user's language (Vietnamese by default).

## Servers

- **`adecos`** (cloud): `https://api.adecos.ai/mcp`, OAuth sign-in with the adecos account. Declared in `.mcp.json`. Claude Code connects it with the plugin; in claude.ai/Desktop chat each user clicks Connect on the plugin's Connectors tab.
- **`adecos-local`** (browser control): runs on the employee's machine from the adecos desktop app. Not part of the plugin — the app's "Kết nối Claude" button shows the config for Claude Desktop and the `claude mcp add-json` command for Claude Code. It does not work on claude.ai web.

## Distribute

Published from the public repo `micace-tech/adecos-claude-plugin` (marketplace `adecos`). User install steps: see the repo README.

- Claude Code: `/plugin install adecos --marketplace micace-tech/adecos-claude-plugin`.
- claude.ai / Desktop: Customize → Plugins → Add marketplace `micace-tech/adecos-claude-plugin`, or upload the release zip. Each user connects the `adecos` server on the plugin's Connectors tab — it is not connected automatically in chat.
- Team/Enterprise org sync from GitHub requires a private repo; with this public repo, admins upload the release zip instead.
- Validate: `claude plugin validate .` (marketplace) and `claude plugin validate plugins/adecos`.

## Maintain

- Time-sensitive numbers live in `skills/*/reference/*.md` with a "checked" date — re-check Google/network pages when they change.
- Labels: **[Google]** = Google Help/policy; **[Industry]** = rule of thumb, not policy.
- Test changes with `evals/scenarios.md` before publishing a new version; bump `version` in `.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json` (repo root), then cut a release with the zip.
