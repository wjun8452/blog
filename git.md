Git常用操作

```
//git remote
git remote -v
git remote add private ssh://git@sh-bitbucket-01.telenav.cn:7999/bitbucket/~junwang_telenavcn/java-sdk-common-2.git
git fetch private
git remote rm private


//rename local branch
git branch -m newname
//删除远端已经不存在的本地分支
git remote prune origin
 
//delete local branch 
git branch -d branch_name 
//delete remote branch
git push origin --delete

//check out remote branch.  
git checkout -t origin/feature/alexa-integration 

//create new branch from an old commit.
git checkout -b release/v3.2 commit   

//checkout a specific version
git checkout <hash>

//push new branch to server
git push --set-upstream origin release/v3.2

//show difference of two commits.  
git diff commit1 commit2 

//reset to commit, 撤销改动以及commit history
git reset --hard commit

//取消提交，将提交移动到缓冲区
git reset HEAD path
//If you want to revert changes made to your working copy, do this:
git checkout .
//If you want to revert changes made to the index (i.e., that you have added), do this. //Warning this will reset all of your unpushed commits to master!:
git reset
//If you want to revert a change that you have committed, do this:
git revert <commit 1> <commit 2>
//If you want to remove untracked files (e.g., new files, generated files):
git clean -f
//Or untracked directories (e.g., new or automatically generated directories):
git clean -fd

//对上一次的提交message做修改
git commit --amend 
//如果上一次的提交已经push了，那么需要加f参数覆盖服务端，不过不建议这么搞
push -f

//tag related
git tag v4.0  //create locally
git push --tags  //push to remote
git tag -d v4.0.0  //local
git push --delete origin v4.0.0  //remote

//clear untracked directories
git clean -df


//rebase before merge your pull request 
//https://github.com/edx/edx-platform/wiki/How-to-Rebase-a-Pull-Request
//https://blog.carbonfive.com/2017/08/28/always-squash-and-rebase-your-git-commits/
//update master, it must be done before merge-base
git checkout master
git pull
git checkout bug_fix_branch
git merge-base bugfix_branch master
git rebase -i ${HASH} --preserve-merges

//if you met error: cannot 'squash' without a previous commit
r 56bcce7 Closes #2774
s e43ceba Lint.py: Replace deprecated link

git push --force





```

### Git flow vs Github flow

https://www.freshconsulting.com/git-development-workflows-git-flow-vs-github-flow/



### Software versioning with git

* [git version]( https://gitversion.readthedocs.io/en/latest/) (https://gitversion.readthedocs.io/en/stable/more-info/how-it-works/)
  * 如果commit被tag过，则首先使用tag来产生版本号。



##Should we test master branch again after relase branch is merged?

After carefully tracing the [GitFlow](http://nvie.com/posts/a-successful-git-branching-model/) diagram, I convinced myself that there should **never** be any conflicts when merging into master (that is if the process is strictly followed). The reason, is because of the timeline:

1. Develop branch is created from Master
2. Features are committed on Develop branch
3. Release branch is created (which includes all the commits from Develop so far)
4. Bugs are fixed in Release branch
5. When ready, the Release branch is merged into Master
6. Master must contain all of the commits from Develop + Release branches. Conflicts should not occur because there was nothing done on Master after Develop branch was created (that's the only way conflicts would happen). In addition, the code at this point should be identical to the latest commit on the Release branch, which is means there is no need for additional testing.

