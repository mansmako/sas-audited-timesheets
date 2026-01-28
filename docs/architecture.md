### Input Layer (Google Sheets)

The Input Layer is the **source of truth** for all timesheet data. It consists of protected admin sheets for hourly rates and open contributor sheets for time entries. Each row records who worked, when they worked, what they did, and the workflow status (Draft → Submitted → Approved).

### Logic Layer (n8n)

The Logic Layer is the **automation brain** that cleans, enriches, and audits the raw spreadsheet data. It normalises emails and dates, merges entries with rates, calculates line‑item totals, evaluates cutoff rules, and generates structured audit events. It also prepares payroll‑ready CSV outputs based only on approved entries.

### Visibility Layer (Slack)

The Visibility Layer is the **communication surface** for the whole system. It publishes weekly summaries and exception alerts (late submissions, post‑cutoff edits, missing entries) into shared Slack channels. This makes the audit trail and operational status visible to managers and operations without them needing to open the spreadsheets or automation tool.
