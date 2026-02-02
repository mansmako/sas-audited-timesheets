# Maintenance Manual – SAS Audited Timesheets

This guide explains how to safely maintain the system without breaking payroll or audit trails.

## 1. Add a New Employee

1. Open the Google Sheet (SAS Weekly Timesheets Master).
2. Go to the **Rates** tab.
3. Insert a new row.
4. Fill in:
   - Employee Email: exact company email (lowercase, no spaces).
   - Hourly Rate: numeric value only (e.g., 500).
   - Effective Date: first date the rate applies (optional but recommended).
5. Save. No change is needed in n8n; the workflow will pick up the new employee.

## 2. Update an Hourly Rate

1. Go to the **Rates** tab.
2. Either:
   - Update the existing row’s Hourly Rate and Effective Date, or
   - Add a new row with the same Employee Email and a newer Effective Date.
3. Inform payroll/operations on Slack:
   - Post a message in `#proj-sas-timesheets-ops` describing the change.
4. For the current cycle, verify that the next payroll CSV reflects the new rate.

## 3. Handle Late Submissions

1. When a late submission alert appears in Slack:
   - Open the **Timesheet_Entries** sheet.
   - Locate the row using Employee Email and Week Start Date.
2. Confirm whether the late entry is acceptable.
3. If acceptable:
   - Leave the data as is; the Audit_Log will record it automatically.
4. If not acceptable:
   - Correct the entry or ask the contributor to fix it.
   - Add a short note in **Audit_Log → Notes** if needed.

## 4. Approve Timesheets

1. Before payroll cut-off, filter **Timesheet_Entries**:
   - Submission Status = Submitted.
2. For each row that is correct:
   - Change Submission Status to Approved.
   - (Apps Script should write Approved By and Approval Timestamp.)
3. After approvals, run the n8n workflow to generate the payroll CSV.

## 5. When Something Looks Wrong

Common symptoms and actions:

- **NaN or wrong totals in CSV**
  - Check Hours Worked and Hourly Rate columns for non-numeric values.
  - Confirm the employee has a rate in the **Rates** tab.

- **Missing rates for some employees**
  - Check that emails in Rates and Timesheet_Entries match in lowercase.
  - Add or fix the employee in the **Rates** tab.

- **Workflow fails / no CSV output**
  - Open n8n, check the execution log for errors.
  - If needed, revert to the previous JSON workflow version in the `n8n` folder.

## 6. Who Owns What

- System owner: responsible for governance, cut-off rules, and approvals.
- Automation owner: maintains n8n workflows and Apps Script.
- Operations: runs the monthly cycle and delivers CSV + Audit_Log to the director.
