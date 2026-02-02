# Architecture – SAS Audited Timesheets

## Input Layer – Google Sheets

- Timesheet_Entries: employees log work (dates, hours, description, status).
- Rates: HR/management define hourly rates per employee.
- Audit_Log: system/appends audit events (late submissions, post-cutoff edits, etc.).

## Logic Layer – n8n

- Normalises emails and dates for reliable joins.
- Merges Timesheet_Entries with Rates to calculate line-item totals.
- Applies cutoff logic to classify on-time vs late.
- Outputs payroll-ready CSVs and audit events.

## Visibility Layer – Slack

- Operational alerts and summaries go to #proj-sas-timesheets-ops.
- Technical failures and issues go to #proj-sas-timesheets-dev.
- Future: announcements in #announce-sas-timesheets.
