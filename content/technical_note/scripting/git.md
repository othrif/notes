---
title: "Working with git"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
# Working with git

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
