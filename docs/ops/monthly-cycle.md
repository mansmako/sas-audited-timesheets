# Monthly Payroll Cycle – SAS Audited Timesheets

This describes how the system runs in a typical cycle.

## 1. Weekly / Monthly rhythm

- Monday morning: n8n trigger runs.
- Scan: identifies who hasn't submitted timesheets and can ping them on Slack.
- Process: pulls all Approved rows from Timesheet_Entries and joins with Rates.
- Output: generates payroll CSV with line-item totals (hours × rate).
- Audit: writes late submissions and post-cutoff edits into Audit_Log.
- Handover: Director receives CSV + Audit_Log for final payment review.

## How to Run a Cycle (Operator Steps)

1. Check Timesheet_Entries for obvious issues (missing weeks/employees).
2. In n8n, open the SAS Timesheets workflow and run it for the current period (Manual Trigger or scheduled run).
3. Download the generated payroll CSV.
4. Export or review Audit_Log for the same period.
5. Send CSV + Audit_Log to the Director for payment review.
