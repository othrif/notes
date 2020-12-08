---
title: "Check package versions"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Check deep learning library versions


```python
!python -c "import tensorflow as tf; print('Tensorflow:', tf.__version__)"
!python -c "import torch; print('Pytorch:', torch.__version__)"
```

    Tensorflow: 2.3.1
    Pytorch: 1.7.0

