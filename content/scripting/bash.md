---
title: "Bash scripting"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Multi-line comments

``` bash
: '
This is a
very neat comment
in bash
'
```

### Output common lines between two files

``` bash 
grep -Fxf file1 file2 # using grep
sort file1 file2 | uniq -d # using sort
```



```python

```
