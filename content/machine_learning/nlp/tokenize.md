---
title: "Processing documents into tokens (tokenization and stop words)"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Tokenization


```python
from nltk.stem.porter import PorterStemmer

porter = PorterStemmer()

def tokenizer(text):
    return text.split()


def tokenizer_porter(text):
    return [porter.stem(word) for word in text.split()]
```


```python
tokenizer('runners like running and thus they run')
```




    ['runners', 'like', 'running', 'and', 'thus', 'they', 'run']




```python
tokenizer_porter('runners like running and thus they run')
```




    ['runner', 'like', 'run', 'and', 'thu', 'they', 'run']



### Stop words


```python
import nltk

nltk.download('stopwords')
```

    [nltk_data] Downloading package stopwords to
    [nltk_data]     /Users/othrif/nltk_data...
    [nltk_data]   Unzipping corpora/stopwords.zip.





    True




```python
from nltk.corpus import stopwords

stop = stopwords.words('english')
[w for w in tokenizer_porter('a runner likes running and runs a lot')[-10:]
if w not in stop]
```




    ['runner', 'like', 'run', 'run', 'lot']


