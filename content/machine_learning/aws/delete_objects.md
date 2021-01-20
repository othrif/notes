---
title: "Delete objects"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### List objects with a match
``` bash 
aws s3 ls s3://mybucket/myfolder --profile prod | grep text_match
aws s3 ls s3://mybucket/myfolder --profile prod | grep text_match > to_delete
```

### Delete single object

``` bash 
aws s3 rm s3://mybucket/myfolder/my_object --profile prod
```

### Delete all objects given a text file containing their paths
``` bash 
for i in `cat to_delete`; do aws s3 rm s3://mybucket/myfolder/${i} --profile prod; done
```



