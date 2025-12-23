# API Database Save Bug
This is a prompt for solving the Task 1 - case with a certain bug, that prevents the API logic from properly saving an update database record.
The prompt:

```
There is this problem: when an update request is made like this:

curl --location --request PUT 'http://localhost:3000/stakeholders/update' \
--header 'x-api-key: xxxxx' \
--header 'Content-Type: application/json' \
--data '{
  "id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "full_name": "Vladyslav Prudius"
}'

the stakeholder has an employee_id FK, and what happens is - it updates the employees table fine, but does NOT update the stakeholders table. 
even though I clearly invoke the upsertStakeholder() function and pass correct data to it. the stakeholders table just stays unchanged.

here are the logs I see during the request:

[2025-10-30 17:21:21 info] applyChanges completed
Built view: {
  email: "vladyslav.prudius@gen.tech",
  full_name: "Vladyslav Prudius",
  ... other fields
  id: "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx,
} 
existing id: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
[2025-10-30 17:21:21 info] Added successfully kind: server, email: vladyslav.prudius@gen.tech, full_name: Vladyslav Prudius, id: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
[2025-10-30 17:21:21 info] Stakeholder updated kind: server, id: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx, full_name: Vladyslav Prudius

the previous name in the db was "Vlad Prudius" but even though logs say update happened and show new name, when I query the stakeholders table - it still has the old name. 
the upsertStakeholder function clearly receives the updated profile with new name, logs say success, but the table is unchanged.

no errors anywhere. endpoint returns 200. employees table updates fine. just stakeholders table doesn't persist the changes.

please research and fix the issue.
```
