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


