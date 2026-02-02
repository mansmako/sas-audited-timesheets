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

   ## How to Run QAT

Environment: use the SAS Weekly Timesheets Master sheet and the current n8n workflow export.

1. Prepare sample data in Timesheet_Entries and Rates (at least 2 employees).
2. Run the n8n workflow manually for a known week.
3. Check the CSV output and Audit_Log.
4. Confirm relevant Slack messages appear (if Slack wiring is configured).

| ID   | Area        | Scenario                 | Expected Result                                     |
|------|-------------|--------------------------|----------------------------------------------------|
| TS-01| Data types  | Hours & rates are numbers| No NaN values in CSV totals.                      |
| TS-02| Merge       | Employee has a rate      | Line-item total = hours × rate.                   |
| TS-03| Normalise   | Email case differences   | Same rate applied regardless of email case.       |
| TS-04| Cutoff      | Before vs after cutoff   | Before = compliant; after = late in Audit_Log.    |
| TS-05| Slack (opt) | Late submission exists   | Late alert shows in ops Slack channel.            |

