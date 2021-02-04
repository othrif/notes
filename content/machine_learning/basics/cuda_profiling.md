---
title: "Profiling GPU with Nvidia tools"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Using Nsight systems

To install Nsight systems:
* Download from Nvidia
* Make executable with `chmod a+x NsightSystems-linux-public-2020.5.1.85-5ee086b.run`
* install with `./NsightSystems-linux-public-2020.5.1.85-5ee086b.run`
* Add to path `export PATH="/home/othrif/setup/nsight-systems-2020.5.1/target-linux-x64:$PATH"`
* Run profiling tool with: `nsys profile ./program`

### Using `nvida-smi`
``` bash 
nvidia-smi -l 1 >> gpu-stats.out
```
