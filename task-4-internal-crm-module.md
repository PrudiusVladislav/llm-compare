# Internal CRM module implementation
This is a prompt for solving the Task 4 - case of a large codebase containing many internal admin panels, developed using custom components, functions, and non-trivial approaches.
The task requires LLM to implement a new module/functionality in one such admin panel, that is expected to cover moren than 2 pages and more than 5 UI components.
The prompt:

```
Task: Implement CRM Events Module for `management` panel

We need to add an Events management section to the `management` admin panel under the CRM group. Look at existing CRM pages for patterns.

Create a page to manage events with:
- Table showing: name, date, description, registration count, and other fields existing in the db schema, that are relevant there
- Filters: by project, by date
- Search: across event name, description, stakeholder names/emails
- Actions: edit event (modal), view participants (navigate to subpage)
- "Add Event" button in header

Event Edit/Create Modal

A form modal for creating and editing events:
- Fields: name, date+time, description, recording link, extra link
- Google Calendar integration: calendar selector → event selector
- Attendance format (online/offline/hybrid), city field visible only for offline/hybrid
- Stakeholders section using shared components

Database: Use `events` and `events_stakeholders` tables. Stakeholders should be replaced on save (delete old + insert new in transaction).

On participants page show all people associated with an event - both registered participants AND attendance-only records (people who attended but didn't register):
- Columns: attended checkbox (editable), name, email, position, grade, company, business, format, whether registered, created date
- Filters: registration status, attendance format, attended yes/no
- Add suitable row color for the participants table
- "Registration Details" action opens modal with full registration info

Attendance import features:
- "Import Attendance" button: opens modal allowing to paste emails, creates attendance records for each

As a reference take a look at other existing admin panels and documentation for share components usage details and patterns.

```
