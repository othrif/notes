---
title: "Titles and labels"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
Seaborn plots create two different types of objects:
- `FacetGrid`: Can create subplots -> `relplot()`, `catplot()`
- `AxesSubplot`: Only creates single plot -> `scatterplot()`, `countplot()`, etc.


- Set title:   
    - `FacetGrid`: `g.fig.suptitle()`
    - `AxesSubplot`: `g.set_title()`
- Set x- and y- labels: `g.set(xlabel='new x-axis label', ylabel='new y-axis label')`
- Rotate x-ticks labels: `plt.xticks(rotation=90)`

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

### Add title and x,y-labels


```python
# Create scatter plot
g = sns.relplot(x="weight", 
                y="horsepower", 
                data=mpg,
                kind="scatter")

# Add a title "Car Weight vs. Horsepower"
g.fig.suptitle('Car Weight vs. Horsepower', y=1.1)
g.set(xlabel='NEW Car Model Year', ylabel='NEW Average MPG')

# Show plot
plt.show()
```


![png](title_label_7_0.png)



```python
# Create line plot
g = sns.lineplot(x="model_year", y="mpg", 
                 data=mpg,
                 hue="origin")

# Add a title "Average MPG Over Time"
g.set_title("Average MPG Over Time")

# Add x-axis and y-axis labels
g.set(xlabel='NEW Car Model Year', ylabel='NEW Average MPG')

# Show plot
plt.show()
```


![png](title_label_8_0.png)


### Rotate tick labels


```python
# Create point plot
sns.catplot(x="origin", 
            y="acceleration", 
            data=mpg, 
            kind="point", 
            join=False, 
            capsize=0.1)

# Rotate x-tick labels
plt.xticks(rotation=90)

# Show plot
plt.show()
```


![png](title_label_10_0.png)

