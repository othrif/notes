---
title: "AWS transcribe service"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Check the status of jobs
``` bash 
aws transcribe list-transcription-jobs --profile prod
aws transcribe list-transcription-jobs --status IN_PROGRESS --profile prod
aws transcribe list-transcription-jobs --status QUEUED --profile prod
aws transcribe list-transcription-jobs --status COMPLETED --profile prod
aws transcribe list-transcription-jobs --status FAILED --profile prod
```
