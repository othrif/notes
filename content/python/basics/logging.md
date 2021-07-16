---
title: "Logging"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### In Jupyter notebook


```python
import logging
logger = logging.getLogger()
logger.setLevel(logging.INFO)

logging.basicConfig(format='%(asctime)s - %(message)s', level=logging.INFO)
logging.info('Admin logged in')
```

    2021-04-20 09:53:24,168 - Admin logged in


### In python script
Won't show result here!


```python
import logging
logging.basicConfig(level=logging.DEBUG)
logging.debug("test")
```
