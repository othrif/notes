---
title: "Embeding a ML model into a Web Application"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Unpickle the classifier


```python
import pickle
import re
import os
from movieclassifier.vectorizer import vect
```

    /Users/othrif/github/notes/content/machine_learning/nlp/movieclassifier/vectorizer.py



```python
clf = pickle.load(open(os.path.join('movieclassifier/pkl_objects', 'classifier.pkl'), 'rb'))
```


```python
import numpy as np
label = {0:'negative', 1:'positive'}

example = ["I love this movie. It's amazing."]
X = vect.transform(example)
print('Prediction: %s\nProbability: %.2f%%' %\
      (label[clf.predict(X)[0]], 
       np.max(clf.predict_proba(X))*100))
```

    Prediction: positive
    Probability: 95.01%



```python
X = vect.transform(["The work that they did with the move is really not up to the standards I expect"])
print('Prediction: %s\nProbability: %.2f%%' %\
      (label[clf.predict(X)[0]], 
       np.max(clf.predict_proba(X))*100))
```

    Prediction: positive
    Probability: 52.79%



```python
X = vect.transform(["they called that a movie!"])
print('Prediction: %s\nProbability: %.2f%%' %\
      (label[clf.predict(X)[0]], 
       np.max(clf.predict_proba(X))*100))
```

    Prediction: negative
    Probability: 68.78%

