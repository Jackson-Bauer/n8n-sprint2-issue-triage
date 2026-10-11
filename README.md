https://github.com/Jackson-Bauer/n8n-sprint2-issue-triage

Purpose: Github issues workflow that creates a ledger and stores information in a database. 

Services: Github, Github CLI, n8n, zapier

Node sequence:
1. Webhook, POST
2. If statement to ensure issues are opened instead of something like being edited
3. Normalize issue: Formats the data and information from the issue.
4. Classify title: Puts the issue into one of four categories
5. Categories: bug, feature, help, other
6. If ledger exists: data table to update existing last seen
7. if ledger row doesnt exist: Creates a new issue row
8. Insert pending ledger row: inserts the row into the data table
9. Intentional failure: check if the issue has a certain sentence in the title and simulate a failure.
10. Update route-log: updates the route log on a success
11. Update route log failed: sets status to failed.

Setup notes:
run gh webhook forward --repo=Jackson-Bauer/n8n-sprint2-issue-triage --events=issues --url=http://localhost:5678/webhook-test/sprint2-issue-triage in github CLI. 
Make sure n8n is waiting on an execution.

