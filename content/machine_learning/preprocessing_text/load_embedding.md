---
title: "Reading embedding file"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
import numpy as np

words = []
vectors = []

with open('wiki-words.emb', 'r') as f:
    print(f)
    for line in f:
        print(line)
        fields = line.split()
        word = fields[0].decode('utf-8')
        vector = np.fromiter((float(x) for x in fields[1:]),
                             dtype=np.float)
        words.append(word)
        vectors.append(vector)

# Matrix of embeddings
matrix = np.array(vectors)
# Vocabulary file
text = '\n'.join(words)
vocab = text.encode('utf-8')
```

    <_io.TextIOWrapper name='wiki-words.emb' mode='r' encoding='UTF-8'>

