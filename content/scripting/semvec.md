---
title: "Semantic versioning with git"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Branch name

`<type>/<name>/<scope>`

Example:
``` bash
feat/myname/stream
```

See: https://semver.org/


#### Commit message header

```
<type>(<scope>): <short summary>
  │       │             │
  │       │             └─⫸ Summary in present tense. Not capitalized. No period at the end.
  │       │
  │       └─⫸ Commit Scope: common|compiler|compiler-cli|core|platform|packaging|changelog|docs|upgrade|etc.                   
  │
  └─⫸ Commit Type: build|ci|docs|feat|fix|perf|refactor|test
```

##### Type

Must be one of the following:

* **build**: Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)
* **ci**: Changes to our CI configuration files and scripts (example scopes: Circle, BrowserStack, SauceLabs)
* **docs**: Documentation only changes
* **feat**: A new feature
* **fix**: A bug fix
* **perf**: A code change that improves performance
* **refactor**: A code change that neither fixes a bug nor adds a feature
* **test**: Adding missing tests or correcting existing tests


