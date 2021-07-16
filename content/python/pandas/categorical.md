---
title: "Categorical data"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Nominal and ordinal features

**Ordinal features**: categorical values that can be sorted, i.e. t-shirt size   
**Nominal features**: don't imply any order, i.e. t-shirt color


```python
import pandas as pd

df = pd.DataFrame([['green', 'M', 10.1, 'class2'],
                   ['red', 'L', 13.5, 'class1'],
                   ['blue', 'XL', 15.3, 'class2']])

df.columns = ['color', 'size', 'price', 'classlabel']
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
      <th>color</th>
      <th>size</th>
      <th>price</th>
      <th>classlabel</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>green</td>
      <td>M</td>
      <td>10.1</td>
      <td>class2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>red</td>
      <td>L</td>
      <td>13.5</td>
      <td>class1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>blue</td>
      <td>XL</td>
      <td>15.3</td>
      <td>class2</td>
    </tr>
  </tbody>
</table>
</div>



### Mapping ordinal features


```python
size_mapping = {'XL': 3,
                'L': 2,
                'M': 1}

df['size'] = df['size'].map(size_mapping)
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
      <th>color</th>
      <th>size</th>
      <th>price</th>
      <th>classlabel</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>green</td>
      <td>1</td>
      <td>10.1</td>
      <td>class2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>red</td>
      <td>2</td>
      <td>13.5</td>
      <td>class1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>blue</td>
      <td>3</td>
      <td>15.3</td>
      <td>class2</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Inverse mapping
inv_size_mapping = {v: k for k, v in size_mapping.items()}
df['size'].map(inv_size_mapping)
```




    0     M
    1     L
    2    XL
    Name: size, dtype: object



### One-hot encoding nominal features

Note you cannot use the `LabelEncoder` since it will introduce an order that did not exist orginally. Use One-Hot encoding


```python
# option1: Pandas
pd.get_dummies(df[['price', 'color', 'size']], drop_first=True)
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
      <th>price</th>
      <th>size</th>
      <th>color_green</th>
      <th>color_red</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10.1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>13.5</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15.3</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# option2: scikit-learn
from sklearn.preprocessing import OneHotEncoder

X = df[['color', 'size', 'price']].values
color_ohe = OneHotEncoder()
color_ohe.fit_transform(X[:, 0].reshape(-1, 1)).toarray()
```




    array([[0., 1., 0.],
           [0., 0., 1.],
           [1., 0., 0.]])



### Encoding class labels


```python
from sklearn.preprocessing import LabelEncoder
# Label encoding with sklearn's LabelEncoder
class_le = LabelEncoder()
y = class_le.fit_transform(df['classlabel'].values)
y
```


```python
# reverse mapping
class_le.inverse_transform(y)
```




    array(['class2', 'class1', 'class2'], dtype=object)


