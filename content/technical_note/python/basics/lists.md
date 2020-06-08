---
title: "Lists, Tuples"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Lists
Lists are mutable


```python
my_list = ['Hello world!', 'banans', 'apples']
```


```python
my_list.append('add one more')
```


```python
my_list
```




    ['Hello world!', 'banans', 'apples', 'add one more']




```python
my_list.extend(['another','even more'])
```


```python
my_list
```




    ['Hello world!', 'banans', 'apples', 'add one more', 'another', 'even more']



#### Access an element


```python
my_list[2]
```




    'apples'




```python
type(my_list)
```




    list



### Subsetting a list
`list[inclusive:exluive]`


```python
my_list[1:3]
```




    ['banans', 'apples']



### Del element


```python
my_list
```




    ['Hello world!', 'banans', 'apples', 'add one more', 'another', 'even more']




```python
del(my_list[1])
```


```python
my_list
```




    ['Hello world!', 'apples', 'add one more', 'another', 'even more']



#### Copy list with `list()`
- `list1 = list0` allows the list to point to the same memory area. Any changes to `list1` will affect `list0`
- To copy `list()` or `[:]`, use the syntax: `list1=list(list0)` or `list1=list0[:]`


```python
# Create list areas
areas = [11.25, 18.0, 20.0, 10.75, 9.50]
print(f'before after: {areas}')

# Create areas_copy
areas_copy1 = areas
areas_copy2 = list(areas)
areas_copy3 = areas[:]

# Change areas_copy
areas_copy1[0] = 1.0
areas_copy2[0] = 2.0
areas_copy3[0] = 3.0

# Print areas
print(f'areas after: {areas}')
print(f'areas_copy1 after: {areas_copy1}')
print(f'areas_copy2 after: {areas_copy2}')
print(f'areas_copy3 after: {areas_copy3}')
```

    before after: [11.25, 18.0, 20.0, 10.75, 9.5]
    areas after: [1.0, 18.0, 20.0, 10.75, 9.5]
    areas_copy1 after: [1.0, 18.0, 20.0, 10.75, 9.5]
    areas_copy2 after: [2.0, 18.0, 20.0, 10.75, 9.5]
    areas_copy3 after: [3.0, 18.0, 20.0, 10.75, 9.5]


### Tuples
Tuples are immutable


```python
t = (0,1,2,3,4)
```

#### Access an element


```python
t[2]
```




    2




```python
type(t)
```




    tuple



#### Special cases


```python
single = (1)
```


```python
type(single)
```




    int




```python
single = (1,)
```


```python
type(single)
```




    tuple



#### Appending


```python
galileo = (['test'],)
```


```python
galileo
```




    (['test'],)




```python
galileo[0].append('another test')
```


```python
galileo
```




    (['test', 'another test'],)




```python
galileo[0].append('yet another test')
```


```python
galileo
```




    (['test', 'another test', 'yet another test'],)



but this is not possible


```python
galileo[0] = ['reset','can\'t be done']
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-34-e195864df4a2> in <module>
    ----> 1 galileo[0] = ['reset','can\'t be done']
    

    TypeError: 'tuple' object does not support item assignment


### Packing and unpacking


```python
date = 6,5,2020
```


```python
type(date)
```




    tuple




```python
day,month,year = date
```


```python
print(f'day={day}, month={month}, year={year}')
```

    day=6, month=5, year=2020



```python
(day,month,year) = date
```

#### Swap variables using unpacking


```python
x,y = 1,2
x,y = y,x
print(f'x={x}, y={y}')
```

    x=2, y=1


#### Remainder


```python
first, *rest = (1,2,3,4,5)
```


```python
print(f'first={first} rest={rest}')
```

    first=1 rest=[2, 3, 4, 5]



```python
first, *middle, last = (1,2,3,4,5)
```


```python
type(middle)
```




    list




```python
print(f'first={first} middle={middle} last={last}')
```

    first=1 middle=[2, 3, 4] last=5



```python
first, *middle, last = [1,2,3,4,5]
```


```python
print(f'first={first} middle={middle} last={last}')
```

    first=1 middle=[2, 3, 4] last=5



```python
a, *b, c = 'HELLOWORLD'
```


```python
b
```




    ['E', 'L', 'L', 'O', 'W', 'O', 'R', 'L']


