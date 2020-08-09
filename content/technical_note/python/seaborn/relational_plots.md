---
title: "Basic plotting of relational plots"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
- `relplot` for relational plots with `scatter`, `line`
- Add 3rd dimension to our plot with:
    - `hue` with different color
    - `row` and `col` to create subplots

Syntax:   
``` python
sns.relplot(x='x_variable_name',
            y='y_variable_name',
            data=pandas_df, 
            kind='scatter')
```

### Necessary includes


```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

### Load data


```python
student_data = pd.read_csv('student.csv')
mpg = pd.read_csv('mpg.csv')
survey_data = pd.read_csv('survey.csv')
```

# Plot with `relplot`

### Scatter plot


```python
sns.relplot(x="absences", y="G3", 
                data=student_data, 
                kind='scatter',
                hue="location", 
                hue_order=['Rural', 'Urban'])
plt.show()
```


![png](relational_plots_8_0.png)


### Subplots in rows and columns


```python
sns.relplot(x="absences", y="G3", 
                data=student_data, 
                kind='scatter',
                col='location',
                col_order=['Rural','Urban'],
                row='sex',
                row_order=['M','F'],
                size='age',
                hue='age',
                style='age', # change the style per additional cateogry
                alpha=0.4    # transparency
           )

# Show plot
plt.show()
```


![png](relational_plots_10_0.png)


# Line plot


```python
sns.relplot(x='model_year', y='mpg', data=mpg, kind='scatter')
plt.show()
```


![png](relational_plots_12_0.png)



```python
# Make the shaded area show the 95% CL 
sns.relplot(x='model_year', y='mpg', data=mpg, kind='line')
plt.show()
```


![png](relational_plots_13_0.png)



```python
# Make the shaded area show the standard deviation
sns.relplot(x="model_year", y="mpg",data=mpg, kind="line", ci='sd')
plt.show()
```


![png](relational_plots_14_0.png)



```python
# Turn off the confidence interval 
sns.relplot(x="model_year", y="mpg",data=mpg, kind="line", ci=None)
plt.show()
```


![png](relational_plots_15_0.png)



```python
# Add markers and make each line have the same style
sns.relplot(x="model_year", y="horsepower", 
            data=mpg, kind="line", 
            ci=None, style="origin", 
            hue="origin", 
            markers=True,
            dashes=False)

plt.show()
```


![png](relational_plots_16_0.png)


# Other formats


```python
# Change the legend order in the scatter plot
sns.scatterplot(x="absences", y="G3", 
                data=student_data, 
                hue="location", 
                hue_order=['Rural', 'Urban'])
plt.show()
```


![png](relational_plots_18_0.png)

