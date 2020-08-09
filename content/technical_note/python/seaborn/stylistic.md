---
title: "Styles, palette, and scales"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Customization

Basics:
- Change background: `sns.set_style()` 
    - styles: 'white', 'dark', 'whitegrid', 'darkgrid', 'ticks'
- Change colors: `sns.set_palette()`
    - Sequential palette: 'Greys', 'Blues', 'PuRd', 'GnBu'
    - Diverging palettes: 'RdBu', 'PRGn', 'RdBu_r', 'PRGn_r'   
- Change scale: `sns.set_context()`
    - context: 'paper', 'notebook', 'talk', 'poster'


Ref:   
- palette: https://seaborn.pydata.org/tutorial/color_palettes.html

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

### Plotting function


```python
def plot_smth(rot):
    # Create a count plot of survey responses
    category_order = ['<2 hours', '2 to 5 hours', '5 to 10 hours', '>10 hours']
    
    sns.catplot(x="study_time", data=student_data, kind="count", order=category_order)
    plt.xticks(rotation=rot)
    plt.show()
```

### Style and Palette


```python
current_palette = sns.color_palette()
sns.palplot(current_palette)
```


![png](stylistic_9_0.png)



```python
# default
plot_smth()
```


![png](stylistic_10_0.png)



```python
# Set the color palette to "Purples"
sns.set_style("whitegrid")
sns.set_palette('Purples')
plot_smth()
```


![png](stylistic_11_0.png)



```python
# Change the color palette to "RdBu"
sns.set_style("whitegrid")
sns.set_palette("RdBu")
plot_smth()
```


![png](stylistic_12_0.png)


### Choose context


```python
# Change the context to "poster"
sns.set_context("talk")
plot_smth(90)
```


![png](stylistic_14_0.png)


### Custom palette


```python
# Set the style to "darkgrid"
sns.set_style('darkgrid')
sns.set_context("poster")

# Set a custom color palette
sns.set_palette(['#39A7D0','#36ADA4'])

# Create the box plot of age distribution by gender
sns.catplot(x="Gender", y="Age", 
            data=survey_data, kind="box")

# Show plot
plt.show()
```


![png](stylistic_16_0.png)

