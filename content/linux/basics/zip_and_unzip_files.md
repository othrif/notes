---
title: "Zip Files and send over ssh"
author: "Othmane Rifki"
date: 2020-04-12T14:41:32+02:00
description: "How to zip and unzip files using the Linux command line."
type: technical_note
draft: false
---

## Remote synch a directory
Compress, copy with ssh, and uncompress:
``` bash 
rsync -arvz -e 'ssh -p <your_port>' --progress <Source DIR> <username>@<your ip>:<Dest DIR>
```

## Zip Files

The `-v` argument is optional, prints an output with the details of the operation.

{{< highlight markdown >}}
gzip regiment.txt battles.txt -v
{{< /highlight >}}
```
regiment.txt:	 -2.2% -- replaced with regiment.txt.gz
battles.txt:	 -5.6% -- replaced with battles.txt.gz
```

## Unzip Files

{{< highlight markdown >}}
gunzip regiment.txt battles.txt
{{< /highlight >}}
