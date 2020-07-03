---
title: "Find the word added to a sentence"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
class Solution():
    
    def __init__(self, sent1,sent2):
        self.sent1=sent1.split()
        self.sent2=sent2.split()
    
    def extra_word(self):
        found={}
        for s1 in self.sent1:
            if s1 in found:
                found[s1]+=1
            else:
                found[s1]=1
        for s2 in self.sent2:
            if s2 in found:
                found[s2]-=1
            else:
                return s2
        print(found)
            
        
```


```python
test1=Solution('this is a dog','this is a a dog')
test1.extra_word()
```

    {'this': 0, 'is': 0, 'a': -1, 'dog': 0}



```python
test2=Solution('Can you solve algorithm questions','Can you solve hard algorithm questions')
test2.extra_word()
```




    'hard'




```python

```
