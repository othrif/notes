---
title: "Confidence Interval"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
from scipy.stats import sem, t
data = [1, 2, 3, 4, 5]
confidence = 0.95
z_score = 2.7764451051977987
sample_mean = 3.0

# Compute the standard error and margin of error
std_err = sem(data)
margin_error = std_err * z_score

# Compute and print the lower threshold
lower = sample_mean - margin_error
print(lower)

# Compute and print the upper threshold
upper = sample_mean + margin_error
print(upper)
```

    1.036756838522439
    4.9632431614775605



```python
from statsmodels.stats.proportion import proportion_confint
# Compute and print the 99% confidence interval
heads = 27
confidence_int = proportion_confint(heads, 50, 0.01)
print(confidence_int)
```

    (0.35844514241179504, 0.721554857588205)



```python
# Compute and print the 90% confidence interval
confidence_int = proportion_confint(heads, 50, 0.1)
print(confidence_int)
```

    (0.42406406993539053, 0.6559359300646095)



```python
from scipy.stats import binom
# Repeat this process 10 times 
heads = binom.rvs(50, 0.5, size=10)
for val in heads:
    confidence_interval = proportion_confint(val, 50, .10)
    print(confidence_interval)
```

    (0.3836912846323326, 0.6163087153676674)
    (0.42406406993539053, 0.6559359300646095)
    (0.2860411978842442, 0.5139588021157558)
    (0.36378436885322046, 0.5962156311467796)
    (0.3440640699353905, 0.5759359300646095)
    (0.42406406993539053, 0.6559359300646095)
    (0.2860411978842442, 0.5139588021157558)
    (0.2860411978842442, 0.5139588021157558)
    (0.5498070827050113, 0.7701929172949887)
    (0.46518968814451866, 0.6948103118554813)


Examine your confidence interval results from the last step. You might see at least one confidence interval that does not contain 0.5, the true population proportion for a fair coin flip. You could decrease the likelihood of this happening by increasing your confidence level or lowering the alpha value.
