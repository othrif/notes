---
title: "Sentiment analysis in text"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Get dataset


```python
import os
import urllib.request
import tarfile
import pandas as pd

source = 'http://ai.stanford.edu/~amaas/data/sentiment/aclImdb_v1.tar.gz'
target = '/tmp/aclImdb_v1.tar.gz'


if not os.path.isdir('/tmp/aclImdb') and not os.path.isfile('/tmp/aclImdb_v1.tar.gz'):
    urllib.request.urlretrieve(source, target)
    
if not os.path.isdir('/tmp/aclImdb'):
    with tarfile.open(target, 'r:gz') as tar:
        tar.extractall()
```


```python
# Build dataframe

basepath = 'aclImdb'

labels = {'pos': 1, 'neg': 0}
df = pd.DataFrame()
for s in ('test', 'train'):
    for l in ('pos', 'neg'):
        path = os.path.join(basepath, s, l)
        for file in sorted(os.listdir(path)):
            with open(os.path.join(path, file), 
                      'r', encoding='utf-8') as infile:
                txt = infile.read()
            df = df.append([[txt, labels[l]]], 
                           ignore_index=True)
df.columns = ['review', 'sentiment']
```


```python
# Shuffling the dataset

import numpy as np

np.random.seed(0)
df = df.reindex(np.random.permutation(df.index))
df.head(3)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>review</th>
      <th>sentiment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>11841</th>
      <td>In 1974, the teenager Martha Moxley (Maggie Gr...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>19602</th>
      <td>OK... so... I really like Kris Kristofferson a...</td>
      <td>0</td>
    </tr>
    <tr>
      <th>45519</th>
      <td>***SPOILER*** Do not read this, if you think a...</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



### Cleaning text with regex


```python
import re
def preprocessor(text):
    text = re.sub('<[^>]*>', '', text)
    emoticons = re.findall('(?::|;|=)(?:-)?(?:\)|\(|D|P)',
                           text)
    text = (re.sub('[\W]+', ' ', text.lower()) +
            ' '.join(emoticons).replace('-', ''))
    return text
```


```python
preprocessor('is seven.<br /><br />Title (Brazil): Not Available')
```




    'is seven title brazil not available'




```python
preprocessor('</a>This :) is :( a test :-)!')
```




    'this is a test :) :( :)'




```python
df['review'] = df['review'].apply(preprocessor)
```


```python
df.head(3)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>review</th>
      <th>sentiment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>11841</th>
      <td>in 1974 the teenager martha moxley maggie grac...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>19602</th>
      <td>ok so i really like kris kristofferson and his...</td>
      <td>0</td>
    </tr>
    <tr>
      <th>45519</th>
      <td>spoiler do not read this if you think about w...</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
