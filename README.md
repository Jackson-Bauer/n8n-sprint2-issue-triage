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
    
Field Mapping:

github_issue_ledger table:
1. issue_key - Unique idempotency key
2. issue url - Clickable link back to the issue
3. title - Classification evidence
4. category - Triage outcome
5. reporeter - basic audit context
6. opened at - event timing
7. last_seen_at - Redelivery evidence
8. route_log_status - internal route log outcome
9. route_name - readable routing result
10. error_note - failure evidence

github_issue_route_log table:
1. issue_key - connects route-log entry to one ledger row
2. category - preserves deterministic classification result\
3. route_name - records the selected route label
4. recorded_at - records when n9n wrote the route-log entry

Classification:
1. Bug - bugs or errors
2. Feature - feature or request
3. Support - help or question
4. other - fallback

Setup notes:
run gh webhook forward --repo=Jackson-Bauer/n8n-sprint2-issue-triage --events=issues --url=http://localhost:5678/webhook-test/sprint2-issue-triage in github CLI. 
Make sure n8n is waiting on an execution.

Test evidence: See test_evidence.md
