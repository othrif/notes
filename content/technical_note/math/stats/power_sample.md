---
title: "How to determine a sample size"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
Let's finish up our dive into statistical tests by performing power analysis to generate needed sample size. Power analysis involves four moving parts:

- Sample size
- Effect size
- Minimum effect
- significance level = P(Type I error) = probability of finding an effect that is not there
- power = 1 - P(Type II error) = probability of finding an effect that is there

### Exercise
In this exercise, you're working with a website and want to test for a difference in conversion rate. Before you begin the experiment, you must decide how many samples you'll need per variant using 5% significance and 95% power.


```python
# Standardize the effect size
from statsmodels.stats.proportion import proportion_effectsize
std_effect = proportion_effectsize(.20, .25)

# Assign and print the needed sample size
from statsmodels.stats.power import  zt_ind_solve_power
sample_size = zt_ind_solve_power(effect_size=std_effect, nobs1=None, alpha=0.05, power=0.95)
print(sample_size)
```

    1807.7621477153323



```python
# Assign and print the needed sample size
from statsmodels.stats.power import  zt_ind_solve_power
sample_size = zt_ind_solve_power(effect_size=std_effect, nobs1=None, alpha=.05, power=0.8)
print(sample_size)
```

    1091.8961587171991


Notice how lowering the power allowed you fewer observations in your sample, yet increased your chance of a Type II error.


```python
sample_sizes = np.array(range(5, 100))
effect_sizes = np.array([0.2, 0.5, 0.8])

# Create results object for t-test analysis
from statsmodels.stats.power import TTestIndPower
results = TTestIndPower()

#Plot the power analysis
import matplotlib.pyplot as plt
results.plot_power(dep_var='nobs', nobs=sample_sizes, effect_size=effect_sizes)
plt.show()
```


![png](power_sample_6_0.png)


Notice that not only does an increase in power result in a larger sample size, but this increase grows exponentially as the minimum effect size is increased.
