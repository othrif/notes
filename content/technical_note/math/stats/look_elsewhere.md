---
title: "Look-elsewhere effect"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
The probability of encountering an error is still extremely high. This is where the Bonferroni correction comes in. While a bit conservative, it controls the family-wise error rate for circumstances like these to avoid the high probability of a Type I error. 


```python
# Print error rate for 60 tests with 5% significance
error_rate = 1 - (.95**(60))
print(error_rate)
```

    0.953930201013048



```python
# Print error rate for 30 tests with 5% significance
error_rate = 1 - (.95**(30))
print(error_rate)
```

    0.7853612360570628



```python
# Print error rate for 10 tests with 5% significance
error_rate = 1 - (.95**(10))
print(error_rate)
```

    0.4012630607616213


### Bonferroni correction
Let's implement multiple hypothesis tests using the Bonferroni correction approach that we discussed in the slides. You'll use the imported `multipletests()` function in order to achieve this.

Use a single-test significance level of .05 and observe how the Bonferroni correction affects our sample list of p-values already created.


```python
from statsmodels.sandbox.stats.multicomp import multipletests
pvals = [.01, .05, .10, .50, .99]

# Create a list of the adjusted p-values
p_adjusted = multipletests(pvals, alpha=0.05, method='bonferroni')

# Print the resulting conclusions
print(p_adjusted[0])

# Print the adjusted p-values themselves 
print(p_adjusted[1])
```

    [ True False False False False]
    [0.05 0.25 0.5  1.   1.  ]


As you can see, the Bonferroni correction did it's job and corrected the family-wise error rate for our 5 hypothesis test results. In the end, only one of the tests remained signficant. There are other methods to do tjhis test:
- Sidak correction
- Step-based procedures 
- Tukey’s procedure
- Dunnet’s correction

