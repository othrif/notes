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

### Tag code version
``` bash 
git checkout main
git pull
git tag -a v0.1.2 -m "tag message"
git push origin v0.1.2 # single tag
# git push origin <tag> # push all tags
```

### Hard reset to a remote repository

If you do something wrong and want to reset:
``` bash 
git fetch origin
git reset --hard origin/main
```

### Push a newly created repo to git
``` bash 
git init
git add .
git commit -m "Initial commit with the basic code structure"
git branch -m master main
git remote add origin https://github.com/<repo>
git push -u origin main
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


### Number of lines of code

Add the following to `cloc-git`
``` bash 
#!/usr/bin/env bash
git clone --depth 1 "$1" temp-linecount-repo &&
  printf "('temp-linecount-repo' will be deleted automatically)\n\n\n" &&
  cloc temp-linecount-repo &&
  rm -rf temp-linecount-repo%
```
Then add it to a folder in your path such as `/usr/local/bin/` and set the proper permission with
``` bash 
chmod a+x cloc-git
```

Find the number of lines with:
``` bash 
cloc-git https://github.com/othrif/repo.git
```


### Avoid needing git token each time

When you want to pull/push from git, you will need your username and token. *Note this is different than your github password*.

To avoid needing to enter your credentials everytime, enable local caching of your credentials:
``` bash 
git config credential.helper store
```

You can also use a public ssh key: copy the contents of `~/.ssh/id_rsa.pub` to [github settings](https://github.com/settings/keys)
