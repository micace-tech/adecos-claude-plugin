---
name: reconciling-affiliate-reports
description: Explains and reconciles differences between affiliate network dashboards, Google Ads and adecos numbers — pending vs approved vs reversed commissions, time-zone and conversion-lag mismatches, refunds, and suspicious values. Use when numbers don't match, "lệch số", revenue dropped after approval, a day looks wrong, or the user asks when commissions become final.
---

# Reconciling affiliate reports

Reply in the user's language (Vietnamese by default).

## Commission lifecycle

Pending → Approved (locked, final) or Reversed/Declined. Reasons for reversal: returns, cancellations, duplicates, fraud, breaking program rules (e.g. forbidden PPC bidding). Refunds can arrive later as **negative** commissions. Validation windows are set per program — see [reference/networks.md](reference/networks.md).

Consequences:
- Judge profit on approved money; pending is a forecast.
- A drop in revenue weeks later is often reversals, not a reporting bug.

## Why "yesterday" differs between systems

1. **Time zones.** Google Ads reports in the ad account's time zone; networks report in their own (Everflow calls this the #1 cause of discrepancies). adecos reads "Yesterday" in Vietnam time (UTC+7).
2. **Conversion lag.** Google Ads conversions can take 15–48 h to appear [Google]; affiliate dashboards also lag.
3. **Date basis.** Click date vs conversion date — Google's default "Conversions" column credits the click date; "Conversions (by conv. time)" credits the conversion date [Google].

Rule: reconcile only days **at least 48 hours old**, on the same date basis and time zone on both sides.

## Anomaly checks [Industry practice, no official standard]

Flag and explain before anyone acts:
- Zero after a run of non-zero days → logout, broken flow, or tracking broke.
- More than ~3× the 7-day median → real spike or wrong date range.
- ~100× or ~1,000× off → decimal/thousands separator, VND vs USD, or EPC shown per 100 clicks (CJ).
- Pending amount that later shrinks → reversals.

adecos already runs its own checks before marking a number "Đã kiểm tra" (date, currency, label, number on page, 30-day range). A "Cần bạn xem" row means one of those failed — see `checking-report-status`.

## Output

State the most likely cause first, the evidence for it, and one concrete check the user can do (which dashboard, which filter, which date). Do not change or save numbers here; corrections go through the app or `collecting-daily-reports`.
