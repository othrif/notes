---
title: "Working with git"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
# Working with git

### Transfer from `github` to `gitlab`
```
git remote add github https://github.com/othrif/vbfmet-recast.git
git push --mirror github
```

#### Git tips

Some basic git commands:

``` bash
 tree -a -I .git
git clone ssh://git@gitlab.cern.ch:7999/othrif/VBFInvAnalysis.git
git status
git add .
git commit -m "change"
git push -u origin master
git pull origin master
git branch -l
git checkout [-b] <branch> # switch or create with -b
git merge <branch>
git ls-files --deleted -z | xargs -0 git rm # in case you removed files
git log # to find all the commits
git checkout a4f5957a0cdcf6d6f3a551f4a0822c0327ce64bc # SHA-1 of the commit
git rev-parse HEAD
```

If you want to create a new branch and check out an old  commit
``` bash
git checkout -b <new branch> <SHA-1>
git add .
git commit -m "added a new branch from old commit"
git push --set-upstream origin <new branch>
```

If you want to bring your branch up-to-date with master
``` bash
git checkout master
git fetch -p origin
git merge origin/master
git checkout <feature-branch>
git merge master
git push origin <feature-branch>
```

If you do something wrong and want to revert to the previous version:
``` bash
 git reset --hard <SHA-1>
 git push origin HEAD:master
```

If you change the repo from different locations, to merge the two:
```
git remote update
git commit -m "fixing conflict"
git merge origin/master
git push
```

Create a new branch from existing branch:
``` bash
git checkout -b new_branch old_branch
```

Merge your completed work on branch <test> with master:
``` bash
git checkout master
git pull origin master
git merge test
git push origin master
```

For gitlab to work with kerboros and mac, you may need:
``` bash
git config --global http.emptyAuth true
```
change remote repostiory from http to ssh
``` bash
git remote set-url origin <ssh address of repo>
```
check if the change happened with:
``` bash
git remote -v
```

Gitlab with Sublime: to push a change do:
ctrl+shift+quick add, ctrl+shift+quick commit, ctrl+shift+push, ^ ` to show/hide console

If you have problems with git ssh keys then do:
``` bash
atlas
lsetup git
ssh-add -t24h
```

check if it is working
``` bash
ssh -v git@gitlab.cern.ch -p 7999
```

Adding submodules:
``` bash
git submodule add https://:@gitlab.cern.ch:8443/atlas-phys-susy-wg/StopPolarizationReweighting.git
cd StopPolarizationReweighting
git checkout 83fec592
cd ..
git add StopPolarizationReweighting .gitmodules
git commit -am "Adding StopPolarizationReweighting submodule"
```
To get the latest submodule from master, cd to submodule
``` bash
git pull origin master
```
## tips from  David ##

- Case when you want to undo what you did BEFORE COMMITTING
``` bash
git reset HEAD --
# or
git reset HEAD filename
```
- Case when you want to undo what you did AFTER COMMITTING but vefore PUSHING
``` bash
git reset HEAD~
```
# to get back to the stage as if you did a clean checkout
``` bash
git reset HEAD~ --hard
```
- If you already PUSHED and wanted to undo the last commit but preserve all the history:
``` bash
git revert <HASH>
```
- Quick tips:
``` bash
git ci: for commit
git st: for status
git lg: to get the nice log
```
- how to branch:
```
git checkout -b mytestbranch
# modify mytestbranch and commit to the branch
git checkout master
# modify master and commit to the branch > now mytestbranch and master diverged
git merge mytestbranch
```
- how to tag:
```bash
git tag -a vXX-220518 -m "test tag version"
git push origin vXX-220518
```
- If you tagged a version of the code then needed to change it, after adding committing, do:
```bash
git tag -f -a <tagname>
git push -f --tags
```
- checkout specific tag
``` bash
git tag
git checkout tags/XYZ
```
- Delete tags
``` bash
git push --delete origin TAGNAME
git tag --delete TAGNAME
```
- go to commit you want then tag it:
``` bash
git checkout <HASH>
git tag <myfirsttag>
git checkout master
```
- if you are in detached state where the HEAD is not pointing to anything, you do:
```
git checkout -b <mynewbranch>
```
- if you push and you realize that your local repo is different from the remote where something else has been pushed
```
git fetch
git merge origin/master
#SIMLAR to
git pull
```
- if you want to checkout a remote branch to have it locally and its name is `oldCodeIn`
```
git checkout oldCodeIn
```
- Force a branch to a different commit or a branch
``` bash
git branch -f master origin/oldCodeIn
```
## Branch and Merging ##
```
git checkout -b myCode-2018-XX-YY
# Modify
git add .
git commit -m "Branch to merge"
git diff origin/master
git push --set-upstream origin myCode-2018-XX-YY
```
Then you are given a link to copy and open in git webpage to perform the merging.

## More tips from David
Having both gitlab and github for one repository:
``` bash
 git remote -v
 git remote rename origin gitlab
 git remote add github https://github.com/othrif/VBFAnalysisCode.git
 git pull gitlab
 git push github
 ```
Now you can pull from gitlab and push to github

To remove a large size file from all your history do:
``` bash
git filter-branch -f --index-filter 'git rm --cached --ignore-unmatch talk/Thesis/lectures/ATLAS_SUSY_sussex.pdf'
```

### Remove submodule

To remove a submodule from a git repository you need to:

Delete the relevant section from the `.gitmodules` file  
Stage the `.gitmodules` changes: `git add .gitmodules`   
Delete the relevant section from `.git/config`   
Run `git rm --cached path_to_submodule` (no trailing slash)    
Run `rm -rf .git/modules/path_to_submodule` (no trailing slash)   
Commit `git commit -m "Removed submodule"`    
Delete the now untracked submodule files `rm -rf path_to_submodule`   

Foldable text:

<details>
  <summary>Title 1</summary>
  <p>Content 1 Content 1 Content 1 Content 1 Content 1</p>
</details>
<details>
  <summary>Title 2</summary>
  <p>Content 2 Content 2 Content 2 Content 2 Content 2</p>
</details>

    Markup : <details>
               <summary>Title 1</summary>
               <p>Content 1 Content 1 Content 1 Content 1 Content 1</p>
             </details>



```python

```
