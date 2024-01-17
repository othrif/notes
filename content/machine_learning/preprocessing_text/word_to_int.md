---
title: "Encode text into integers and pad with zeros
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Encode text into integers using Counter()


```python
import pandas as pd 

# Get data

my_data = {'sentiment': [1, 0, 0, 1, 0],
 'review': ['This movie is great',
  'OK... so... I really like Kris Kristofferson!',
  'SPOILER: Do not watch this movie!',
  'hi for all the people who have seen this wonderful art.',
  'I recently bought the DVD, it is a waste.']}

df = pd.DataFrame(my_data)
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
      <th>sentiment</th>
      <th>review</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>This movie is great</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>OK... so... I really like Kris Kristofferson!</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>SPOILER: Do not watch this movie!</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>hi for all the people who have seen this wonde...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>I recently bought the DVD, it is a waste.</td>
    </tr>
  </tbody>
</table>
</div>




```python
from collections import Counter
from string import punctuation

# Seperate words and count each word's occurence
counts = Counter()
for i, review in enumerate(df['review']):
    text = ''.join([c if c not in punctuation else ' '+c+' ' for c in review]).lower()
    df.loc[i,'review'] = text
    counts.update(text.split())
```


```python
# Map each unique word to an integer
word_counts = sorted(counts, key=counts.get, reverse=True)
print(word_counts[:5])
word_to_int = {word: ii for ii, word in enumerate(word_counts, 1)}
word_to_int
```

    ['.', 'this', 'movie', 'is', 'i']





    {'.': 1,
     'this': 2,
     'movie': 3,
     'is': 4,
     'i': 5,
     '!': 6,
     'the': 7,
     'great': 8,
     'ok': 9,
     'so': 10,
     'really': 11,
     'like': 12,
     'kris': 13,
     'kristofferson': 14,
     'spoiler': 15,
     ':': 16,
     'do': 17,
     'not': 18,
     'watch': 19,
     'hi': 20,
     'for': 21,
     'all': 22,
     'people': 23,
     'who': 24,
     'have': 25,
     'seen': 26,
     'wonderful': 27,
     'art': 28,
     'recently': 29,
     'bought': 30,
     'dvd': 31,
     ',': 32,
     'it': 33,
     'a': 34,
     'waste': 35}




```python
# Convert text to integers based on previous mapping
mapped_reviews = []
for review in df['review']:
    mapped_reviews.append([word_to_int[word] for word in review.split()])
print(df.loc[0,'review'], '->', mapped_reviews[0])
```

    this movie is great -> [2, 3, 4, 8]


### Pad with zeros for fixed input


```python
import numpy as np

# Define same length sequence
# if sequence length < 200: left-pad with zeros
# if sequence length > 200: use the last 200 elements 

sequence_length = 10
sequences = np.zeros((len(mapped_reviews), sequence_length), dtype=int)
sequences
```




    array([[0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
           [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
           [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
           [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
           [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]])




```python
mapped_reviews
```




    [[2, 3, 4, 8],
     [9, 1, 1, 1, 10, 1, 1, 1, 5, 11, 12, 13, 14, 6],
     [15, 16, 17, 18, 19, 2, 3, 6],
     [20, 21, 22, 7, 23, 24, 25, 26, 2, 27, 28, 1],
     [5, 29, 30, 7, 31, 32, 33, 4, 34, 35, 1]]




```python
for i, row in enumerate(mapped_reviews):
    review_arr = np.array(row)
    sequences[i, -len(row):] = review_arr[-sequence_length:]
sequences
```




    array([[ 0,  0,  0,  0,  0,  0,  2,  3,  4,  8],
           [10,  1,  1,  1,  5, 11, 12, 13, 14,  6],
           [ 0,  0, 15, 16, 17, 18, 19,  2,  3,  6],
           [22,  7, 23, 24, 25, 26,  2, 27, 28,  1],
           [29, 30,  7, 31, 32, 33,  4, 34, 35,  1]])


