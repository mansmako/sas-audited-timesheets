# Timesheet_Entries Sheet Structure

Google Sheet: SAS Weekly Timesheets Master
Tab name: Timesheet_Entries

| Column | Name                | Example                 | Notes                                  |
|--------|---------------------|-------------------------|----------------------------------------|
| A      | Employee Name       | Jane Doe               | Free text.                             |
| B      | Employee Email      | jane@example.com       | Used as key to join with Rates.       |
| C      | Week Start Date     | 2026-02-03             | Monday of the week.                   |
| D      | Work Date           | 2026-02-05             | Must fall within Week Start + 0..6.   |
| E      | Hours Worked        | 8                      | Number between 0 and 24.              |
| F      | Work Description    | Deploy infra changes   | Optional but recommended.             |
| G      | Submission Status   | Draft / Submitted / Approved | Lifecycle state.              |
| H      | Submission Timestamp| 2026-02-03 17:05       | Filled by script on Submitted.        |
| I      | Last Edit Timestamp | 2026-02-03 17:07       | Auto-updated on any edit.             |
| J      | Approved By         | Team Lead Name         | Manager identity.                     |
| K      | Approval Timestamp  | 2026-02-04 09:12       | Filled when status becomes Approved.  |
