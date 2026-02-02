# Monthly Payroll Cycle – SAS Audited Timesheets

This describes how the system runs in a typical cycle.

## 1. Weekly / Monthly rhythm

- Monday morning: n8n trigger runs.
- Scan: identifies who hasn't submitted timesheets and can ping them on Slack.
- Process: pulls all Approved rows from Timesheet_Entries and joins with Rates.
- Output: generates payroll CSV with line-item totals (hours × rate).
- Audit: writes late submissions and post-cutoff edits into Audit_Log.
- Handover: Director receives CSV + Audit_Log for final payment review.
