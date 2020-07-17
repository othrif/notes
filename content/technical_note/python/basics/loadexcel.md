---
title: "Loading an excel file"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Concept
use pandas to import Excel spreadsheets and how to list the names of the sheets in any loaded .xlsx file.


```python
# Import pandas
import pandas as pd

# Assign spreadsheet filename: file
file = 'battledeath.xlsx'

# Load spreadsheet: xls
xls = pd.ExcelFile(file)

# Print sheet names
print(xls.sheet_names)

```

    ['2002', '2004']



```python
# Load a sheet into a DataFrame by name: df1
df1 = xls.parse('2004')
print(df1.head())

# Load a sheet into a DataFrame by index: df2
df2 = xls.parse(0)
print(df2.head())
```

      War(country)      2004
    0  Afghanistan  9.451028
    1      Albania  0.130354
    2      Algeria  3.407277
    3      Andorra  0.000000
    4       Angola  2.597931
      War, age-adjusted mortality due to       2002
    0                        Afghanistan  36.083990
    1                            Albania   0.128908
    2                            Algeria  18.314120
    3                            Andorra   0.000000
    4                             Angola  18.964560


### Customize the spreadsheet import


```python
# Parse the first sheet and rename the columns: df1, skip first row and rename columns
df1 = xls.parse(0, skiprows=[0], names=['Country','AAM due to War (2002)'])

# Print the head of the DataFrame df1
print(df1.head())

# Parse the first column of the second sheet and rename the column: df2
df2 = xls.parse(1, usecols=[0], skiprows=[0], names=['Country'])

# Print the head of the DataFrame df2
print(df2.head())

```

                   Country  AAM due to War (2002)
    0              Albania               0.128908
    1              Algeria              18.314120
    2              Andorra               0.000000
    3               Angola              18.964560
    4  Antigua and Barbuda               0.000000
                   Country
    0              Albania
    1              Algeria
    2              Andorra
    3               Angola
    4  Antigua and Barbuda



```python

```
