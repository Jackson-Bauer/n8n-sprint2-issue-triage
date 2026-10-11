
**Purpose**
This runbook explains how to operate, use, and shutdown / start the n8n issue triage.
Action: Explain what this document is for.
Result: Someone with no experience can start and use the workflow.
Evidence: README.md, test_evidence.md, JSON export

**Normal Operation**
Actions:
Start n8n at localhost 5678
Open the workflow and start listening for an event
Go to powershell and turn on Github CLI by typing the command found in README
Create a Github issue before checking the data tables in n8n.
Expected result: 
New rows in the data tables for the issues. 
Evidence location: test_evidence.md, JSON export

**Duplicate Delivery**
Actions: 
In Github, go to settings, webhooks, and select redeliver. Ensure n8n is waiting on a new event.
Check the datatables to ensure only last access changed.
Expected result:
Only last_seen_at is updated and no new row is created.
Evidence: test_evidence.md

**Route-log failrue**
Actions:
Create a new issue with "intentional route-log failure test" in the body. 
Execute the workflow, check the data tables
Expected result:
route_log_status = failed, error_note confirming
Evidence location:
test_evidence.md
**Recovery action**
Action:
When route_log_status is failed, read the error note.
Check the executions log in n8n to find the node that caused the issue
Fix the issue, save the workflow, and then finish the workflow. 
Can also delete the bad row and redo. 
Expected result:
A fixed row in both tables
Evidence location:
The data tables in n8n
**Safe shutdown**
Action:
Control + C in the powershell to turn off Github CLI
In n8n quit listening for events
Expected results:
no more events will occur in n8n 
new issues in Github will not trigger the webhook.
Evidence location:
test_evidence.md for canceling Github CLI
**What this prototype does not test**
1. Webhook Authentication
2. More than 3 types of events
3. Non-opened issues
4. Data backups
5. Hosting
