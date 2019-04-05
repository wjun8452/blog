Git常用操作

```
//delete local branch 
git branch -d branch_name 

//check out remote branch.  
git checkout -t origin/feature/alexa-integration 

//create new branch from an old commit.
git checkout -b release/v3.2 commit   

//push new branch to server
git push --set-upstream origin release/v3.2

//show difference of two commits.  
git diff commit1 commit2 

//reset to commit
git reset -hard commit

//push the rest to remote
git push origin master --force

//create a tag
git tag v3.2-lw
git push --tags

//revert uncommited staging files


//update master, it must be done before merge-base
git checkout master
git pull

//find fork-point commit
git merge-base bugfix_branch master

//rebase
git rebase -i commit_displayed_above master
git push --force



```
