---
title: "Working with git"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Bring your branch up-to-date with master
``` bash
git checkout master
git fetch -p origin
git merge origin/master
git checkout <feature-branch>
git merge master
git push origin <feature-branch>
```

### Create a new branch and check out an old  commit
``` bash
git checkout -b <new branch> <SHA-1>
git add .
git commit -m "added a new branch from old commit"
git push --set-upstream origin <new branch>
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

### Transfer from `github` to `gitlab`
```
git remote add github https://github.com/othrif/vbfmet-recast.git
git push --mirror github
```



```python

```
