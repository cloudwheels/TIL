---
tags:
  - git
categories:
  - development
excerpt: >-
   Safely removing git history
---
Deleting the  `.git`  folder may cause problems in your git repository. If you want to delete all your commit history but keep the code in its current state, it is very safe to do it as in the following:

1.  Checkout
    
    `git checkout --orphan latest_branch`
    
2.  Add all the files
    
    `git add -A`
    
3.  Commit the changes
    
    `git commit -am "commit message"`
    
4.  Delete the branch
    
    `git branch -D master`
    
5.  Rename the current branch to master
    
    `git branch -m master`
    
6.  Finally, force update your repository
    
    `git push -f origin master`
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY0MTY2NzA1MF19
-->