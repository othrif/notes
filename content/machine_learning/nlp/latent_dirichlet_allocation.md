---
title: "Topic modeling with Latent Dirichlet Allocation"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Get dataset


```python
import os
import urllib.request
import gzip
import pandas as pd

source = 'https://github.com/rasbt/python-machine-learning-book-3rd-edition/raw/master/ch08/movie_data.csv.gz'
target = '/tmp/movie_data.csv.gz'


if not os.path.isfile(target):
    print ("download start!")
    filename, headers = urllib.request.urlretrieve(source, filename=target)
    print ("download complete!")
 
if not os.path.isfile('/tmp/movie_data.csv'):
    with gzip.open(target, 'rb') as in_f, \
                open('/tmp/movie_data.csv', 'wb') as out_f:
            out_f.write(in_f.read())
            print (target + " extraction complete!")
    
df = pd.read_csv(target, encoding='utf-8')
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
      <th>0</th>
      <td>In 1974, the teenager Martha Moxley (Maggie Gr...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>OK... so... I really like Kris Kristofferson a...</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>***SPOILER*** Do not read this, if you think a...</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
from sklearn.feature_extraction.text import CountVectorizer

count = CountVectorizer(stop_words='english',
                        max_df=.1,
                        max_features=5000)
X = count.fit_transform(df['review'].values)
```


```python
from sklearn.decomposition import LatentDirichletAllocation

lda = LatentDirichletAllocation(n_components=10,
                                random_state=123,
                                learning_method='batch')
X_topics = lda.fit_transform(X)
```


```python
lda.components_.shape
```




    (10, 5000)




```python
lda.components_[0].argsort()[:-n_top_words - 1:-1]
```




    array([4962, 2896,  379, 3891, 4301])




```python
n_top_words = 5
feature_names = count.get_feature_names()

for topic_idx, topic in enumerate(lda.components_):
    print("Topic %d:" % (topic_idx + 1))
    print(" ".join([feature_names[i]
                    for i in topic.argsort()\
                        [:-n_top_words - 1:-1]]))
```

    Topic 1:
    worst minutes awful script stupid
    Topic 2:
    family mother father children girl
    Topic 3:
    american war dvd music tv
    Topic 4:
    human audience cinema art sense
    Topic 5:
    police guy car dead murder
    Topic 6:
    horror house sex girl woman
    Topic 7:
    role performance comedy actor performances
    Topic 8:
    series episode war episodes tv
    Topic 9:
    book version original read novel
    Topic 10:
    action fight guy guys cool


Based on reading the 5 most important words for each topic, we may guess that the LDA identified the following topics:

1. Generally bad movies (not really a topic category)      
1. Movies about families      
1. War movies      
1. Art movies      
1. Crime movies      
1. Horror movies      
1. Comedies      
1. Movies somehow related to TV shows     
1. Movies based on books     
1. Action movies     

To confirm that the categories make sense based on the reviews, let's plot 5 movies from the horror movie category (category 6 at index position 5):


```python
X_topics.shape
```




    (50000, 10)




```python
horror = X_topics[:, 5].argsort()[::-1]

for iter_idx, movie_idx in enumerate(horror[:3]):
    print('\nHorror movie #%d:' % (iter_idx + 1))
    print(df['review'][movie_idx][:300], '...')

```

    
    Horror movie #1:
    House of Dracula works from the same basic premise as House of Frankenstein from the year before; namely that Universal's three most famous monsters; Dracula, Frankenstein's Monster and The Wolf Man are appearing in the movie together. Naturally, the film is rather messy therefore, but the fact that ...
    
    Horror movie #2:
    Okay, what the hell kind of TRASH have I been watching now? "The Witches' Mountain" has got to be one of the most incoherent and insane Spanish exploitation flicks ever and yet, at the same time, it's also strangely compelling. There's absolutely nothing that makes sense here and I even doubt there  ...
    
    Horror movie #3:
    <br /><br />Horror movie time, Japanese style. Uzumaki/Spiral was a total freakfest from start to finish. A fun freakfest at that, but at times it was a tad too reliant on kitsch rather than the horror. The story is difficult to summarize succinctly: a carefree, normal teenage girl starts coming fac ...

