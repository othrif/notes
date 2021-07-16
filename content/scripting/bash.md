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

### Replace white space with underscore in filename
``` bash 
for f in *; do mv "$f" `echo $f | tr ' ' '_'`; done
```

### Processing a large number of files
To avoid the error `Argument list too long`:
``` bash 
ls | xargs -n 32 -P 8 cat >> ../saved_output
```
The xargs utility will take the output of ls, break it into chunks of 32 (32 arguments) and spawn up to 8 concurrent cat processes.  cat will be respawned  as long as their is data coming from ls.

### Randomly select N files
``` bash 
ls | shuf -n 50
```
