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
        tar.extractall(path='/tmp/')
```


```python
# Build dataframe

basepath = '/tmp/aclImdb'

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
df
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
      <th>0</th>
      <td>I went and saw this movie last night after bei...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Actor turned director Bill Paxton follows up h...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>As a recreational golfer with some knowledge o...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>I saw this film in a sneak preview, and it is ...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bill Paxton has taken the true story of the 19...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>49995</th>
      <td>Towards the end of the movie, I felt it was to...</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49996</th>
      <td>This is the kind of movie that my enemies cont...</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49997</th>
      <td>I saw 'Descent' last night at the Stockholm Fi...</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49998</th>
      <td>Some films that you pick up for a pound turn o...</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49999</th>
      <td>This is one of the dumbest films, I've ever se...</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>50000 rows × 2 columns</p>
</div>




```python
# Shuffling the dataset

import numpy as np

np.random.seed(0)
df = df.reindex(np.random.permutation(df.index))
df.to_csv('/tmp/movie_data.csv', index=False, encoding='utf-8')
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
    text = re.sub('<[^>]*>', '', text) # removes anything that is between <>
    emoticons = re.findall('(?::|;|=)(?:-)?(?:\)|\(|D|P)', # checkout https://regexr.com/: captures emoticons with the pattern (:|;|=) + (- or not) + ()
                           text)
    text = (re.sub('[\W]+', ' ', text.lower()) + # matches any non-word character
            ' '.join(emoticons).replace('-', ''))
    return text
```


```python
preprocessor('is seven.<br /><br />Title (Brazil): Not Available')
```


```python
preprocessor('</a>This :) is :( a test :-)!')
```


```python
df['review'] = df['review'].apply(preprocessor)
```


```python
df.head(3)
```

### Processing documents into tokens


```python
from nltk.stem.porter import PorterStemmer
from nltk.corpus import stopwords

porter = PorterStemmer()

def tokenizer(text):
    return text.split()

def tokenizer_porter(text):
    return [porter.stem(word) for word in text.split()]

stop = stopwords.words('english')
```

### Train logistic regression model


```python
X_train = df.loc[:25000, 'review'].values
y_train = df.loc[:25000, 'sentiment'].values
X_test = df.loc[25000:, 'review'].values
y_test = df.loc[25000:, 'sentiment'].values
```


```python
from sklearn.pipeline import Pipeline
from sklearn.linear_model import LogisticRegression
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.model_selection import GridSearchCV

tfidf = TfidfVectorizer(strip_accents=None,
                        lowercase=False,
                        preprocessor=None)

param_grid = [{'vect__ngram_range': [(1, 1)], # 1
               'vect__stop_words': [stop, None], # 2
               'vect__tokenizer': [tokenizer, tokenizer_porter], # 2
               'clf__penalty': ['l1', 'l2'], # 2
               'clf__C': [1.0, 10.0, 100.0]}, # 3
              {'vect__ngram_range': [(1, 1)], # 1
               'vect__stop_words': [stop, None], # 2
               'vect__tokenizer': [tokenizer, tokenizer_porter], # 2
               'vect__use_idf':[False], # 1
               'vect__norm':[None], # 1
               'clf__penalty': ['l1', 'l2'], # 2
               'clf__C': [1.0, 10.0, 100.0]}, # 3
              ]

lr_tfidf = Pipeline([('vect', tfidf),
                     ('clf', LogisticRegression(random_state=0, solver='liblinear'))])

gs_lr_tfidf = GridSearchCV(lr_tfidf, param_grid,
                           scoring='accuracy',
                           cv=5,
                           verbose=2,
                           n_jobs=-1)
```

There are 2*2*2*3*5 + 2*2*2*3*5 = 240 models to fit. **THIS TAKES SO LONG!!!!**


```python
gs_lr_tfidf.fit(X_train, y_train)
```


```python
print('Best parameter set: %s ' % gs_lr_tfidf.best_params_)
print('CV Accuracy: %.3f' % gs_lr_tfidf.best_score_)
```


```python
clf = gs_lr_tfidf.best_estimator_
print('Test Accuracy: %.3f' % clf.score(X_test, y_test))
```


```python

```
