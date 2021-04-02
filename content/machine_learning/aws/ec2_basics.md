---
title: "EC2 basics"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Describe instances
``` bash 
aws ec2 describe-instances --profile personal
```

### ssh to an EC2 instance
``` bash 
chmod 600 </path/my-key-pair.pem>
ssh -i </path/my-key-pair.pem> ec2-user@<Public IPv4 DNS>
```
Run `aws configure` to put in your credentials to have access to s3.
