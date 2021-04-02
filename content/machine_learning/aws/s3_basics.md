---
title: "S3 Copy from / to / between aws"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Copying directory to s3 with structure intact
``` bash 
aws s3 sync myDir s3://mybucket --profile prototype
```

### Recursively copying S3 objects to a local directory

``` bash 
aws s3 cp s3://mybucket . --recursive --profile prototype
```

### Recursively copying local files to S3
``` bash 
aws s3 cp myDir s3://mybucket/ --recursive --exclude "*.jpg" --profile prototype
```

### Recursively copying S3 objects to another bucket
``` bash 
aws s3 cp s3://mybucket/ s3://mybucket2/ --recursive --exclude "another/*" --profile prototype
```

### Copying an S3 object to a local file
``` bash 
aws s3 cp s3://mybucket/test.txt test2.txt --profile prototype
```

### Copying a local file to S3
``` bash 
aws s3 cp test.txt s3://mybucket/test2.txt --profile prototype
```

### Copying a file from S3 to S3
``` bash 
aws s3 cp s3://mybucket/test.txt s3://mybucket/test2.txt --profile prototype
```

### Rename folder in S3
``` bash 
aws s3 mv s3://mybucket/folder_name_from/ s3://mybucket/folder_name_to/ --recursive --profile prototype
```
