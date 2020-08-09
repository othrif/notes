---
title: "Basic plotting of categorical plots"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
- `catplot` for categorical plots with `bar`, `count`, `box`, `point`
- Add 3rd dimension to our plot with:
    - `hue` with different color
    - `row` and `col` to create subplots

Syntax:   
``` python
sns.catplot(x='x_variable_name',
            y='y_variable_name',
            data=pandas_df, 
            kind='bar')
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

# Plot with `catplot`

### Count plot (histogram)


```python
survey_data['Mathematics'].unique()
survey_data['Interested in Math'] = survey_data['Mathematics']>3
```


```python
# Create column subplots based on age category
sns.catplot(y="Internet usage", data=survey_data,
            kind="count",
            col='Loneliness')

plt.show()
```


![png](categorical_plot_9_0.png)


### Bar plot


```python
# Create a bar plot of interest in math, separated by gender
sns.catplot(x='Gender', y='Interested in Math', data=survey_data, kind='bar')

# Show plot
plt.show()
```


![png](categorical_plot_11_0.png)



```python
# Create bar plot of average final grade in each study category
sns.catplot(x='study_time', y='G3', data=student_data, kind='bar',
           order=['<2 hours', '2 to 5 hours', '5 to 10 hours', '>10 hours'],
           ci=None)

plt.show()
```


![png](categorical_plot_12_0.png)


### Box plot


```python
# Plot the data that we want to convert to a box plot.
sns.catplot(x='study_time', y='G3', data=student_data)

# Show plot
plt.show()
```


![png](categorical_plot_14_0.png)



```python
# Specify the category ordering
study_time_order = ["<2 hours", "2 to 5 hours", 
                    "5 to 10 hours", ">10 hours"]

# Create a box plot and set the order of the categories
sns.catplot(x='study_time', y='G3', data=student_data, kind='box', order=study_time_order)

# Show plot
plt.show()
```


![png](categorical_plot_15_0.png)



```python
# Create a box plot with subgroups and omit the outliers
sns.catplot(x='internet', y='G3', data=student_data, hue='location', kind='box', sym='')

# Show plot
plt.show()
```


![png](categorical_plot_16_0.png)



```python
# Set the whiskers to 0.5 * IQR
sns.catplot(x="romantic", y="G3",
            data=student_data,
            kind="box", whis=0.5)

# Show plot
plt.show()
```


![png](categorical_plot_17_0.png)



```python
# Extend the whiskers to the 5th and 95th percentile
sns.catplot(x="romantic", y="G3",
            data=student_data,
            kind="box",
            whis=[5,95])

# Show plot
plt.show()
```


![png](categorical_plot_18_0.png)



```python
# Set the whiskers at the min and max values
sns.catplot(x="romantic", y="G3",
            data=student_data,
            kind="box",
            whis=[0, 100])

# Show plot
plt.show()
```


![png](categorical_plot_19_0.png)


### Point plot


```python
# Remove the lines joining the points
sns.catplot(x="famrel", y="absences",
            data=student_data,
            kind="point",
            capsize=0.2,
            join=False)
            
# Show plot
plt.show()
```


![png](categorical_plot_21_0.png)



```python
# Import median function from numpy
import numpy as np

# Plot the median number of absences instead of the mean
sns.catplot(x="romantic", y="absences",
            data=student_data,
            kind="point",
            hue="school",
            ci=None,
            estimator=np.median)

# Show plot
plt.show()
```


![png](categorical_plot_22_0.png)


It looks like students in romantic relationships have a higher average and median number of absences in the GP school, but this association does not hold for the MS school.

# Other formats


```python
# Create a dictionary mapping subgroup values to colors
palette_colors = {'Rural': "green", 'Urban': "blue"}

# Create a count plot of school with location subgroups
sns.countplot(x='school', data=student_data, hue='location', palette=palette_colors)

plt.show()
```


![png](categorical_plot_25_0.png)

