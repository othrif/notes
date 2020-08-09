---
title: "A tf-idf word-frequency array and mining Wikipedia"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
tf–idf or TFIDF, short for term frequency–inverse document frequency, is a numerical statistic that is intended to reflect how important a word is to a document in a collection or corpus.

### TfidfVectorizer
`TfidfVectorizer` from sklearn. It transforms a list of documents into a word frequency array, which it outputs as a csr_matrix. It has fit() and transform() methods like other sklearn objects.


```python
documents = ['cats say meow', 'dogs say woof', 'dogs chase cats']
```


```python
# Import TfidfVectorizer
from sklearn.feature_extraction.text import TfidfVectorizer

# Create a TfidfVectorizer: tfidf
tfidf = TfidfVectorizer() 

# Apply fit_transform to document: csr_mat
csr_mat = tfidf.fit_transform(documents)

# Print result of toarray() method
print(csr_mat.toarray())

# Get the words: words
words = tfidf.get_feature_names()

# Print words
print(words)

```

    [[0.51785612 0.         0.         0.68091856 0.51785612 0.        ]
     [0.         0.         0.51785612 0.         0.51785612 0.68091856]
     [0.51785612 0.68091856 0.51785612 0.         0.         0.        ]]
    ['cats', 'chase', 'dogs', 'meow', 'say', 'woof']


### Mining Wikipedia


```python
import pandas as pd
from scipy.sparse import csr_matrix

df = pd.read_csv('wikipedia/wikipedia-vectors.csv', index_col=0)
articles = csr_matrix(df.transpose())
titles = list(df.columns)
```


```python
# Perform the necessary imports
from sklearn.decomposition import TruncatedSVD
from sklearn.cluster import KMeans
from sklearn.pipeline import make_pipeline

# Create a TruncatedSVD instance: svd
svd = TruncatedSVD(n_components=50)

# Create a KMeans instance: kmeans
kmeans = KMeans(n_clusters=6)

# Create a pipeline: pipeline
pipeline = make_pipeline(svd, kmeans)

```


```python
# Import pandas
import pandas as pd

# Fit the pipeline to articles
pipeline.fit(articles)

# Calculate the cluster labels: labels
labels = pipeline.predict(articles)

# Create a DataFrame aligning labels and titles: df
df = pd.DataFrame({'label': labels, 'article': titles})

# Display df sorted by cluster label
print(df.sort_values('label'))

```

        label                                        article
    59      0                                    Adam Levine
    50      0                                   Chad Kroeger
    51      0                                     Nate Ruess
    52      0                                     The Wanted
    53      0                                   Stevie Nicks
    58      0                                         Sepsis
    55      0                                  Black Sabbath
    56      0                                       Skrillex
    57      0                          Red Hot Chili Peppers
    54      0                                 Arctic Monkeys
    21      1                             Michael Fassbender
    28      1                                  Anne Hathaway
    27      1                                 Dakota Fanning
    26      1                                     Mila Kunis
    25      1                                  Russell Crowe
    24      1                                   Jessica Biel
    23      1                           Catherine Zeta-Jones
    22      1                              Denzel Washington
    20      1                                 Angelina Jolie
    29      1                               Jennifer Aniston
    0       2                                       HTTP 404
    1       2                                 Alexa Internet
    2       2                              Internet Explorer
    3       2                                    HTTP cookie
    4       2                                  Google Search
    5       2                                         Tumblr
    6       2                    Hypertext Transfer Protocol
    7       2                                  Social search
    8       2                                        Firefox
    9       2                                       LinkedIn
    38      3                                         Neymar
    37      3                                       Football
    36      3              2014 FIFA World Cup qualification
    35      3                Colombia national football team
    39      3                                  Franck Ribéry
    33      3                                 Radamel Falcao
    32      3                                   Arsenal F.C.
    31      3                              Cristiano Ronaldo
    30      3                  France national football team
    34      3                             Zlatan Ibrahimović
    49      4                                       Lymphoma
    48      4                                     Gabapentin
    46      4                                     Prednisone
    45      4                                    Hepatitis C
    47      4                                          Fever
    43      4                                       Leukemia
    42      4                                    Doxycycline
    41      4                                    Hepatitis B
    40      4                                    Tonsillitis
    44      4                                           Gout
    19      5  2007 United Nations Climate Change Conference
    10      5                                 Global warming
    11      5       Nationally Appropriate Mitigation Action
    12      5                                   Nigel Lawson
    13      5                               Connie Hedegaard
    14      5                                 Climate change
    15      5                                 Kyoto Protocol
    16      5                                        350.org
    17      5  Greenhouse gas emissions by the United States
    18      5  2010 United Nations Climate Change Conference

