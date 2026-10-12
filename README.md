Repo: https://github.com/Jackson-Bauer/n8n-sprint2-issue-triage

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
12. 
Field Mapping:
github_issue_ledger table:
issue_key - Unique idempotency key
issue url - Clickable link back to the issue
title - Classification evidence
category - Triage outcome
reporeter - basic audit context
opened at - event timing
last_seen_at - Redelivery evidence
route_log_status - internal route log outcome
route_name - readable routing result
error_note - failure evidence
-----------
github_issue_route_log table:
issue_key - connects route-log entry to one ledger row
category - preserves deterministic classification result
route_name - records the selected route label
recorded_at - records when n9n wrote the route-log entry

Classification:
1. Bug - bugs or errors
2. Feature - feature or request
3. Support - help or question
4. other - fallback

Setup notes:
run gh webhook forward --repo=Jackson-Bauer/n8n-sprint2-issue-triage --events=issues --url=http://localhost:5678/webhook-test/sprint2-issue-triage in github CLI. 
Make sure n8n is waiting on an execution.

Test evidence: See test_evidence.md
