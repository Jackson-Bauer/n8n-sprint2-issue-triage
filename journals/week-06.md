
**One capability to be added next:**
I think the next thing to be added is extending beyond just opened issues. Labels, edited, closed, and reopened. They are all important parts of these issues that are ignored by the webhook. 

Adding would not be that difficult to pull off, I would merely have to update the "opened action" if node. I could change the if statement to a switch of sorts that separates each different issue type. Then it would just be recreating the existing workflow again for each case. 

Data fields would be the only part that makes the extension harder. My first idea would be to create entirely new tables for each type, but that would result in closer to 10+ tables. The only other option I can think of is to add even more columns to the already existing tables, but that also has its downsides. 
