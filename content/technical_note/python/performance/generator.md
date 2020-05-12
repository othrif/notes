---
title: "List comprehension and generator expressions"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### List comprehension
It more compact notation, compare the following for-loops expression:


```python
lst=[[1,2,3],[4,5,6]]
for row_idx, row_val in enumerate(lst):
    for col_idx, col_val in enumerate(row_val): 
        lst[row_idx][col_idx] += 1
lst
```




    [[2, 3, 4], [5, 6, 7]]



with the list comprehension expression, the above for loops simplifies greatly:


```python
lst=[[1,2,3],[4,5,6]]
[[cell + 1 for cell in row] for row in lst]
```




    [[2, 3, 4], [5, 6, 7]]



the following summation code will build a full list of squares in memory, iterate over those values, and, when the reference is no longer needed, delete the list:


```python
sum([x*x for x in range(10)])
```




    285



### Generator expressions
Many of the use cases do not need to have a full list created in memory. Instead, they only need to iterate over the elements one at a time. Memory is conserved by using a generator expression instead:


```python
sum(x*x for x in range(10))
```




    285



### More examples
Check here https://www.python.org/dev/peps/pep-0289/   


```python

```
