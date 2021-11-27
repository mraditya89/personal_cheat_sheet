###### tags : `tutorial`
# Git Cheat Sheet
## A. Basic Command
### 1. Initialization, Status, Log
- Initialize git
  command : `git init`
- Check status
  command : `git status`
- Show log
  command : `git log`
- Show log with graph, in oneline, and all branch
  command : `git log --graph --all --oneline --decorate`
  
### 2. Add, Commit
- stage changes a specific file 
  command : `git add <file_name>`
- stage chages all file 
  command : `git add .`
- Commit changes
  command : `git commit -m "a message"`
- Rename last commit
  command : `git commit --amend "do awesome stuff"`
- Add changes but not create new commit
  command : `git commit --amend`

### 3. Checkout
- Back to specific commit 
  command : `git checkout <commit_id>`
- Back to Last commit / remove modification
  command : `git checkout .`
- Move to Another branch
  command : `git checkout <branch_name>`
  
### 4. Branch
- Show branch list
  command : `git branch`
- Create a New Branch
  command : `git branch dev` 
- Move to "dev" branch
  command : `git checkout dev`
- Delete "dev" branch
  command : `git branch -d dev`
  
### 5. Merge
- Merge a branch to "master" branch. 
  - step 0 : Make sure you are in master branch. 
  - step 1 : Merge "dev" branch to master with type `git merge dev`
  - step 2 : If there is a conflict, resolve the conflict manually
- Resolve Conflict
  - step 1 : Resolve conflict manually
  - step 2 : `git add .`
  - step 3 : `git commit -m "resolve conflict"`
 
  
### 6. Working with Remote Repo
- Add remote repo
  command : `git remote add <alias> <remote_url>`
- Update log changes
  command : `git fetch`
- Update local branch
  command : `git pull <alias> <branch>`
- Update all branch 
  command : `git push <remote> --all`
- Update remote branch
  command : `git push <alias> <branch>`
- Clone a repo
  command : `git clone <repo_url>`

### 7. Reset
- reset staging files to unstage
  command : `git reset`
- back to desire commit, but keep changes on staging area
  command : `git reset <commit_destination_id> --soft`
- back to desire commit but keep changes on the working area: 
  command : `git reset <commit_destination_id>`
- back to desire commit and remove changes: `git reset <commit_destination_id> --hard`

## B. Problem Solving
#### 1. Git work flow
Work flow 1 (Solo):
- step 1 : create "feature" branch for development. 
- step 2 : do awesome development on branch "feature"
- step 3 : debugging / unit testing
- step 4 : commit development
- step 5 : merge to master branch
- step 6 : push to remote repo


Workflow 2 (simple-collab)
- step 1 : create feature-1 branch
- step 2 : do awesome development on feature-1 branch
- step 3 : before pushing to remote repo:
   - checkout to master branch and pull
   - checkout to feature-1 branch, use rebase : `git rebase master`
   - resolve conflict
   - on branch master rebase again : `git reabse feature-1`
- step 4 : push master to remote
- 
Workflow 3 (collab)
Developer :
- step 1 : create feature-1 branch
- step 2 : do awesome development on feature-1 branch
- step 3 : before pushing to remote repo:
   - checkout to master branch and pull
   - checkout to feature-1 branch, merge master
   - resolve conflict
   - push branch to repo
- step 4 : create pull request on github

Manager :
- step 5 : review by manager
- step 6 : merge branch

Developer :
- step 7 : in master branch, pull 
- step 8 : do another development



#### 2. I can't move to another branch because i still working on branch "dev". Git asks me to commit  or stash it, before checking out.
Solution 1:
- step 1 : stash changes `git stash`
- step 2 : you can move to the desire branch
- step 3 : back to previous branch : `git checkout dev`
- step 4 : show stash list : `git stash list`
- step 5 : apply changes : `git stash apply <stash_id>` 
- step 6 : delete stash_id : `git stash drop <stash_id>` 
> note you can do apply and delete stash_id in one command : `git stash pop`

Solution 2:
- step 1 : add to staging area and commit it. 
- step 2 : go to desire branch
- step 3 : back to previous branch
- step 4 : when you want to commit, you can use git commit --amend to overwrite the previous commit
<!-- # 
# case 2: remove commit, commit history still exists
got revert <commit_id>
Note: appear vim text editor, quit :wq

#case 6 : paste commit
git cherry-pick <commit_id>
 -->
 
## C. Awesome Links
1. Git tutorial : https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud
2. Git visualization : https://git-school.github.io/ 
