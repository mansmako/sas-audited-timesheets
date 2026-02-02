# Audit_Log Sheet Structure

Google Sheet: SAS Weekly Timesheets Master
Tab name: Audit_Log

| Column | Name       | Example                       | Notes                                                       |
|--------|------------|-------------------------------|-------------------------------------------------------------|
| A      | Timestamp  | 2026-02-03 17:32              | When the audit event was recorded.                         |
| B      | User       | jane@example.com              | Actor who triggered the event (employee or system).        |
| C      | Event Type | LATE_SUB / POST_CUT_EDIT ...  | Code for the audit flag or event.                          |
| D      | Sheet Row ID | 42                          | Row number or unique ID from Timesheet_Entries.            |
| E      | Notes      | Edited hours from 6 → 9       | Free text with additional context for the event.           |
