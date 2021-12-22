---
title: "Bag of words"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Transforming documents into feature vectors

By calling the fit_transform method on CountVectorizer, we just constructed the vocabulary of the bag-of-words model and transformed the following three sentences into sparse feature vectors


```python
import numpy as np
from sklearn.feature_extraction.text import CountVectorizer

count = CountVectorizer()
docs = np.array([
        'The sun is shining',
        'The weather is sweet',
        'The sun is shining, the weather is sweet, and one and one is two'])
bag = count.fit_transform(docs)
```

Content of the vocabulary:


```python
print(count.vocabulary_)
```

    {'the': 6, 'sun': 4, 'is': 1, 'shining': 3, 'weather': 8, 'sweet': 5, 'and': 0, 'one': 2, 'two': 7}


Each index position in the feature vectors shown here corresponds to the integer values that are stored as dictionary items in the CountVectorizer vocabulary.
Those values in the feature vectors are also called the raw term frequencies: tf (t,d)—the number of times a term t occurs in a document d.


```python
print(bag.toarray())
```

    [[0 1 0 1 1 0 1 0 0]
     [0 1 0 0 0 1 1 0 1]
     [2 3 2 1 1 1 2 1 1]]


### Assessing word relevancy via term frequency-inverse document frequency

When we are analyzing text data, we often encounter words that occur across multiple documents from both classes. Those frequently occurring words typically don't contain useful or discriminatory information. Frequency-inverse document frequency (tf-idf) that can be used to downweight those frequently occurring words in the feature vectors. 

The tf-idf can be defined as the product of the term frequency and the inverse document frequency:   
    $\text{tf-idf}(t,d)=\text{tf (t,d)}\times \text{idf}(t,d)$   

The inverse document frequency **idf(t, d)** can be calculated as:    
$\text{idf}(t,d) = \text{log}\frac{n_d}{1+\text{df}(d, t)}$    
where $n_d$ is the total number of documents, and **df(d, t)** is the number of documents *d* that contain the term *t*. 


```python
np.set_printoptions(precision=2)
from sklearn.feature_extraction.text import TfidfTransformer

tfidf = TfidfTransformer(use_idf=True, 
                         norm='l2', 
                         smooth_idf=True)
print(tfidf.fit_transform(count.fit_transform(docs))
      .toarray())

```

    [[0.   0.43 0.   0.56 0.56 0.   0.43 0.   0.  ]
     [0.   0.43 0.   0.   0.   0.56 0.43 0.   0.56]
     [0.5  0.45 0.5  0.19 0.19 0.19 0.3  0.25 0.19]]


Equivalent to


```python
tfidf = TfidfTransformer(use_idf=True, norm=None, smooth_idf=True)
raw_tfidf = tfidf.fit_transform(count.fit_transform(docs)).toarray()[-1]  # Last document
raw_tfidf
```




    array([3.39, 3.  , 3.39, 1.29, 1.29, 1.29, 2.  , 1.69, 1.29])




```python
l2_tfidf = raw_tfidf / np.sqrt(np.sum(raw_tfidf**2))
l2_tfidf
```




    array([0.5 , 0.45, 0.5 , 0.19, 0.19, 0.19, 0.3 , 0.25, 0.19])



### Combine both bagging and tfidf


```python
from sklearn.feature_extraction.text import TfidfVectorizer
tfidf = TfidfVectorizer(strip_accents=None,
                        lowercase=False,
                        preprocessor=None)
tfidf.fit_transform(docs).toarray()
```




    array([[0.43, 0.  , 0.43, 0.  , 0.56, 0.56, 0.  , 0.  , 0.  , 0.  ],
           [0.43, 0.  , 0.43, 0.  , 0.  , 0.  , 0.56, 0.  , 0.  , 0.56],
           [0.15, 0.5 , 0.45, 0.5 , 0.19, 0.19, 0.19, 0.25, 0.25, 0.19]])



### Calculation by hand

Calculation of the tf-idf computed by scikitlear is:   
$\text{idf}(t,d) = \text{log}\frac{1 + n_d}{1+\text{df}(d, t)}$     
$\text{tf-idf}(t,d)=\text{tf (t,d)}\times \left( 1 + \text{idf}(t,d) \right)$   

**tf(t,d)**: How many times the term t appears in document d.   
**df(d,t)**: How many documents have the term t.   

In the example of the 3rd document, the term 'and' appears 2 times:   
$\text{tf}('and', d3) = 2$  
$\text{df}(d, 'and')  = 1$  
$\text{idf}('and', d3) = \text{log}\frac{1 + 3}{1 + 1} = 0.69$  
$\text{tf-idf}('and', d3) = 2 * (1 + log(2)) = 3.39$  


```python
tf_and = 2
df_and = 1
n_docs = 3
idf_and = np.log((1 + n_docs) / (1 + df_and))
tfidf_and = tf_and * (1 + idf_and)
print('tf-idf of term "and" = %.2f' % tfidf_and)
```

    tf-idf of term "and" = 3.39


Repeating the caclucation bove, we obtain:

$\text{tf-idf}(d3) = [3.39, 3.  , 3.39, 1.29, 1.29, 1.29, 2.  , 1.69, 1.29]$


```python
raw_tfidf = np.array([3.39, 3.  , 3.39, 1.29, 1.29, 1.29, 2.  , 1.69, 1.29])
```


```python
print(f'tf-idf normalized is: {raw_tfidf / np.sqrt(np.sum(raw_tfidf**2))}')
```

    tf-idf normalized is: [0.5  0.44 0.5  0.19 0.19 0.19 0.3  0.25 0.19]

