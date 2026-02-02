# QAT Plan – SAS Audited Timesheets

## Scope

- Google Sheets: Timesheet_Entries, Rates, Audit_Log.
- n8n: normalisation, rate merge, cutoff logic, CSV export.
- Slack: notifications for submissions and exceptions.

## Core Test Cases

1. **NaN Bug Prevention**
   - Setup: enter numeric Hours Worked and Hourly Rate.
   - Action: run the workflow.
   - Expected: line-item totals are numeric, no "NaN" values.

2. **Zero-Total Bug Prevention**
   - Setup: ensure Rates contains an hourly rate for the test employee.
   - Action: run workflow on entries for that employee.
   - Expected: lineItemTotal > 0 for rows with hours; merge is correctly configured.

3. **Case-Sensitivity Leak**
   - Setup: enter Employee Email in different cases (e.g., Mako@... and mako@...).
   - Action: run the workflow.
   - Expected: both resolve to the same rate after normalisation (toLowerCase).

4. **Cutoff Definition**
   - Setup: create two submissions, one before and one after the cutoff.
   - Action: run the workflow.
   - Expected: before-cutoff = compliant; after-cutoff = late flag written to Audit_Log.

5. **Slack Visibility**
   - Setup: ensure Slack credentials are configured.
   - Action: run a cycle with at least one late submission.
   - Expected: exception message appears in the correct Slack channel.
