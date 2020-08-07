---
title: "Importing SAS and Stata files"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### SAS files
SAS: Statistical Analysis System   
Used for business analytics and biostatistics   
File extension: `.sasb7dat`


```python
import pandas as pd
import matplotlib.pyplot as plt
from sas7bdat import SAS7BDAT


# Save file to a DataFrame: df_sas
with SAS7BDAT('sales.sas7bdat') as file:
    df_sas = file.to_data_frame()

# Print head of DataFrame
print(df_sas.head())

# Plot histogram of DataFrame features (pandas and pyplot already imported)
pd.DataFrame.hist(df_sas[['S','P']])
plt.ylabel('count')
plt.show()
```

         YEAR     P           S
    0  1950.0  12.9  181.899994
    1  1951.0  11.9  245.000000
    2  1952.0  10.7  250.199997
    3  1953.0  11.3  265.899994
    4  1954.0  11.2  248.500000



![png](loadsas_2_1.png)


### Stata files
Stata: Statistical Analysis System   
Used for 
File extension: `.dta`


```python
# Import pandas
import pandas as pd

# Load Stata file into a pandas DataFrame: df
df = pd.read_stata('disarea.dta')

# Print the head of the DataFrame df
print(df.head())

# Plot histogram of one column of the DataFrame
pd.DataFrame.hist(df[['disa10']])
plt.xlabel('Extent of disease')
plt.ylabel('Number of countries')
plt.show()

```

      wbcode               country  disa1  disa2  disa3  disa4  disa5  disa6  \
    0    AFG           Afghanistan   0.00   0.00   0.76   0.73    0.0   0.00   
    1    AGO                Angola   0.32   0.02   0.56   0.00    0.0   0.00   
    2    ALB               Albania   0.00   0.00   0.02   0.00    0.0   0.00   
    3    ARE  United Arab Emirates   0.00   0.00   0.00   0.00    0.0   0.00   
    4    ARG             Argentina   0.00   0.24   0.24   0.00    0.0   0.23   
    
       disa7  disa8  ...  disa16  disa17  disa18  disa19  disa20  disa21  disa22  \
    0   0.00    0.0  ...     0.0     0.0     0.0    0.00    0.00     0.0    0.00   
    1   0.56    0.0  ...     0.0     0.4     0.0    0.61    0.00     0.0    0.99   
    2   0.00    0.0  ...     0.0     0.0     0.0    0.00    0.00     0.0    0.00   
    3   0.00    0.0  ...     0.0     0.0     0.0    0.00    0.00     0.0    0.00   
    4   0.00    0.0  ...     0.0     0.0     0.0    0.00    0.05     0.0    0.00   
    
       disa23  disa24  disa25  
    0    0.02    0.00    0.00  
    1    0.98    0.61    0.00  
    2    0.00    0.00    0.16  
    3    0.00    0.00    0.00  
    4    0.01    0.00    0.11  
    
    [5 rows x 27 columns]



![png](loadsas_4_1.png)



```python

```
