---
title: "Check if 2 strings are anagrams"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
class Solution():
    
    def __init__(self,s1,s2):
        self.s1=s1
        self.s2=s2
        
    def anagram(self):
        c1={}
        c2={}
        return self.countchar(self.s1)==self.countchar(self.s2)
    
    def countchar(self,s):
        h={}
        for c in s:
            if c in h:
                h[c]+=1
            else:
                h[c]=1
        return h
        
    
```


```python
word = Solution('word', 'wodr')
word.anagram()
```




    True




```python
word = Solution('dog', 'dogg')
word.anagram()
```




    False


