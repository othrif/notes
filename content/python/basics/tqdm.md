---
title: "tqdm cool progress meter"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### In shell


```python
# Number of bytes per second
!seq 9999999 | tqdm --bytes | wc -l
```

    109MB [00:02, 47.8MB/s] 
     9999999



```python
# Number of lines per second
!seq 9999999 | tqdm | wc -l
```

    9999999it [00:03, 2633163.40it/s]
     9999999



```python
# Number of lines per second
!seq 9999999 | tqdm --bytes --total 99999999 | wc -l
```

     59%|██████████████████████▍               | 56.3M/95.4M [00:01<00:00, 46.9MB/s]^C
     66%|████████████████████████▉             | 62.6M/95.4M [00:01<00:00, 45.7MB/s]
    Traceback (most recent call last):
      File "/Users/othrif/.pyenv/versions/3.8.5/bin/tqdm", line 8, in <module>


### In python


```python
from tqdm import tqdm
from time import sleep

for i in tqdm(range(100)):
    sleep(0.01)
```

    100%|██████████| 100/100 [00:01<00:00, 86.17it/s]

