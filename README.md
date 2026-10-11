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

Evidence 
<img width="928" height="730" alt="image" src="https://github.com/user-attachments/assets/f25df83d-5f34-43ed-9e85-d0964f5a2780" />
<img width="931" height="750" alt="image" src="https://github.com/user-attachments/assets/4630bf86-039e-4561-a26f-4070738f0ea2" />
<img width="990" height="527" alt="image" src="https://github.com/user-attachments/assets/56a1e41c-aee3-4957-9ad0-2a59036c2924" />
<img width="945" height="761" alt="image" src="https://github.com/user-attachments/assets/73437c83-1b27-41c7-8adc-5a1228f29a6f" />
<img width="900" height="420" alt="image" src="https://github.com/user-attachments/assets/28aaf5db-98fe-4826-82c1-992e84a019be" />
<img width="968" height="270" alt="image" src="https://github.com/user-attachments/assets/69b24a22-5166-4493-ab94-fc5459346c69" />
<img width="922" height="731" alt="image" src="https://github.com/user-attachments/assets/521895c2-cf59-4635-852b-9c37dda2011d" />
<img width="1022" height="696" alt="image" src="https://github.com/user-attachments/assets/6a84a272-2634-4696-a5b6-4b7151726954" />

