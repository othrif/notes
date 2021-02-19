---
title: "Split text by punctuation"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Using `nltk`

Download `nltk` models with the one-time setup and get the `punkt` model for sentence parsing (also called sentence tokenizing):


```python
import nltk
nltk.download()
```

    NLTK Downloader
    ---------------------------------------------------------------------------
        d) Download   l) List    u) Update   c) Config   h) Help   q) Quit
    ---------------------------------------------------------------------------


    Downloader>  q





    True



then use it as:


```python
import nltk.data
tokenizer = nltk.data.load('tokenizers/punkt/english.pickle')
s = "hello, world! It's me, X! Testing this tool."
tokenizer.tokenize(str(s))
```




    ['hello, world!', "It's me, X!", 'Testing this tool.']


