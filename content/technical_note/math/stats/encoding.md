---
title: "Encoding techniques"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Centrality
label encoding and one-hot encoding. 


```python
import pandas as pd
```


```python
laptops = pd.read_csv('laptops.csv' , encoding='latin-1', index_col=0) # added encoding because of errors
laptops = laptops.loc[laptops['Company'].isin(['Apple', 'Dell', 'Lenovo'])] 
```


```python
laptops.head()
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
      <th>Company</th>
      <th>Product</th>
      <th>TypeName</th>
      <th>Inches</th>
      <th>ScreenResolution</th>
      <th>Cpu</th>
      <th>Ram</th>
      <th>Memory</th>
      <th>Gpu</th>
      <th>OpSys</th>
      <th>Weight</th>
      <th>Price_euros</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Apple</td>
      <td>MacBook Pro</td>
      <td>Ultrabook</td>
      <td>13.3</td>
      <td>IPS Panel Retina Display 2560x1600</td>
      <td>Intel Core i5 2.3GHz</td>
      <td>8GB</td>
      <td>128GB SSD</td>
      <td>Intel Iris Plus Graphics 640</td>
      <td>macOS</td>
      <td>1.37kg</td>
      <td>1339.69</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Apple</td>
      <td>Macbook Air</td>
      <td>Ultrabook</td>
      <td>13.3</td>
      <td>1440x900</td>
      <td>Intel Core i5 1.8GHz</td>
      <td>8GB</td>
      <td>128GB Flash Storage</td>
      <td>Intel HD Graphics 6000</td>
      <td>macOS</td>
      <td>1.34kg</td>
      <td>898.94</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Apple</td>
      <td>MacBook Pro</td>
      <td>Ultrabook</td>
      <td>15.4</td>
      <td>IPS Panel Retina Display 2880x1800</td>
      <td>Intel Core i7 2.7GHz</td>
      <td>16GB</td>
      <td>512GB SSD</td>
      <td>AMD Radeon Pro 455</td>
      <td>macOS</td>
      <td>1.83kg</td>
      <td>2537.45</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Apple</td>
      <td>MacBook Pro</td>
      <td>Ultrabook</td>
      <td>13.3</td>
      <td>IPS Panel Retina Display 2560x1600</td>
      <td>Intel Core i5 3.1GHz</td>
      <td>8GB</td>
      <td>256GB SSD</td>
      <td>Intel Iris Plus Graphics 650</td>
      <td>macOS</td>
      <td>1.37kg</td>
      <td>1803.60</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Apple</td>
      <td>MacBook Pro</td>
      <td>Ultrabook</td>
      <td>15.4</td>
      <td>IPS Panel Retina Display 2880x1800</td>
      <td>Intel Core i7 2.2GHz</td>
      <td>16GB</td>
      <td>256GB Flash Storage</td>
      <td>Intel Iris Pro Graphics</td>
      <td>Mac OS X</td>
      <td>2.04kg</td>
      <td>2139.97</td>
    </tr>
  </tbody>
</table>
</div>



### Label encoding


```python
from sklearn import preprocessing
# Create the encoder and print our encoded new_vals
encoder = preprocessing.LabelEncoder()
new_vals = encoder.fit_transform(laptops['Company'])
print(new_vals)
```

    [0 0 0 0 0 0 0 1 0 0 1 0 2 1 2 1 1 0 1 1 1 0 2 1 1 1 0 2 1 2 1 1 1 2 2 1 1
     2 1 1 0 2 1 1 1 1 1 1 2 2 1 2 1 1 2 1 1 1 2 2 2 2 1 1 2 2 1 1 2 1 2 1 2 1
     1 2 1 1 2 1 2 2 1 1 2 2 1 2 1 1 1 2 2 1 2 1 1 1 2 1 1 2 1 1 2 1 2 1 0 1 2
     1 2 1 2 1 1 1 2 2 0 1 2 1 1 2 2 2 1 2 2 2 2 2 1 2 2 1 2 2 2 2 2 2 1 1 2 2
     2 1 2 1 1 1 2 2 1 2 1 1 1 1 2 1 1 1 2 2 1 2 1 2 1 2 1 2 2 2 2 1 1 2 1 2 2
     1 2 2 2 1 2 2 2 2 1 1 1 2 2 1 1 1 1 2 2 2 2 2 2 1 2 2 1 1 1 2 1 1 1 2 2 1
     2 1 1 1 2 1 1 1 2 2 1 1 2 2 2 2 2 2 2 2 2 2 2 1 1 1 2 1 1 2 2 2 1 1 1 1 1
     2 1 1 2 2 2 2 1 1 2 1 2 2 1 1 2 2 2 2 2 1 1 1 1 2 2 2 1 2 2 2 2 1 1 1 2 2
     2 1 1 1 1 1 2 1 2 2 1 1 2 2 1 2 2 1 2 2 2 2 1 1 1 2 1 1 2 2 1 2 2 2 1 2 1
     1 2 2 2 2 1 2 2 2 2 1 2 2 2 1 1 1 2 1 2 2 2 1 2 1 1 1 1 2 2 1 1 1 2 2 1 2
     2 2 1 2 1 1 1 1 1 2 1 2 2 2 1 2 2 0 2 1 2 1 1 1 1 1 2 1 1 2 1 1 2 2 2 1 2
     2 2 1 2 1 1 1 1 2 1 1 2 2 2 1 2 1 2 2 2 1 1 2 1 1 2 2 1 1 1 1 1 2 2 2 1 2
     2 1 1 2 1 2 1 2 2 1 1 1 2 2 1 2 1 1 2 1 1 1 2 1 1 1 2 1 1 1 2 1 2 1 2 1 1
     2 2 1 1 1 2 1 1 1 1 2 2 2 2 1 1 1 1 1 1 1 1 0 1 2 2 2 2 2 2 2 1 2 1 1 1 1
     1 2 1 2 1 2 2 1 2 1 2 2 2 2 2 1 2 1 2 2 2 1 1 2 2 2 2 1 2 2 2 2 2 2 2 2 1
     1 1 2 0 1 2 1 2 1 1 1 2 0 1 2 2 2 1 1 1 1 2 2 1 0 1 2 2 1 1 2 1 1 2 2 1 1
     2 2 1 1 2 1 2 2 2 1 1 2 1 2 2 2 1 1 2 1 2 2 2]


### One-hot encode


```python
# One-hot encode Company for laptops2
laptops2 = pd.get_dummies(data=laptops, columns=['Company'])
laptops2.head()
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
      <th>Product</th>
      <th>TypeName</th>
      <th>Inches</th>
      <th>ScreenResolution</th>
      <th>Cpu</th>
      <th>Ram</th>
      <th>Memory</th>
      <th>Gpu</th>
      <th>OpSys</th>
      <th>Weight</th>
      <th>Price_euros</th>
      <th>Company_Apple</th>
      <th>Company_Dell</th>
      <th>Company_Lenovo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>MacBook Pro</td>
      <td>Ultrabook</td>
      <td>13.3</td>
      <td>IPS Panel Retina Display 2560x1600</td>
      <td>Intel Core i5 2.3GHz</td>
      <td>8GB</td>
      <td>128GB SSD</td>
      <td>Intel Iris Plus Graphics 640</td>
      <td>macOS</td>
      <td>1.37kg</td>
      <td>1339.69</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Macbook Air</td>
      <td>Ultrabook</td>
      <td>13.3</td>
      <td>1440x900</td>
      <td>Intel Core i5 1.8GHz</td>
      <td>8GB</td>
      <td>128GB Flash Storage</td>
      <td>Intel HD Graphics 6000</td>
      <td>macOS</td>
      <td>1.34kg</td>
      <td>898.94</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MacBook Pro</td>
      <td>Ultrabook</td>
      <td>15.4</td>
      <td>IPS Panel Retina Display 2880x1800</td>
      <td>Intel Core i7 2.7GHz</td>
      <td>16GB</td>
      <td>512GB SSD</td>
      <td>AMD Radeon Pro 455</td>
      <td>macOS</td>
      <td>1.83kg</td>
      <td>2537.45</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>MacBook Pro</td>
      <td>Ultrabook</td>
      <td>13.3</td>
      <td>IPS Panel Retina Display 2560x1600</td>
      <td>Intel Core i5 3.1GHz</td>
      <td>8GB</td>
      <td>256GB SSD</td>
      <td>Intel Iris Plus Graphics 650</td>
      <td>macOS</td>
      <td>1.37kg</td>
      <td>1803.60</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>MacBook Pro</td>
      <td>Ultrabook</td>
      <td>15.4</td>
      <td>IPS Panel Retina Display 2880x1800</td>
      <td>Intel Core i7 2.2GHz</td>
      <td>16GB</td>
      <td>256GB Flash Storage</td>
      <td>Intel Iris Pro Graphics</td>
      <td>Mac OS X</td>
      <td>2.04kg</td>
      <td>2139.97</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
