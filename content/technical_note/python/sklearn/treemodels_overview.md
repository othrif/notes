---
title: "Overview of Tree-based Models"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
# Decision-Tree or CART (Classification And Regression Tree)

### Decision tree

![Decision Tree](decisiontree.png)

### Information gain

![Information Gain](informationgain.png)

# k-Fold CV

![](figs/kfoldcv.png)

CV error = $\frac{E_1 + E_2 + \cdots + E_10}{10}$

# Ensemble learning

![](figs/ensemblelearning.png)

### Meta-model = hard voting

![](figs/hardvoting.png)

# Bagging

### Bootstrap

![](figs/bootstrap.png)

### Bagging training

![](figs/baggingtraining.png)

### Bagging prediction
- Classification: Aggregates predictions by majority voting
- Regression: Aggregates predictions through averaging.

![](figs/baggingprediction.png)

### Out of Bag evaluation

![](figs/oob.png)

# Random Forests

### Training

![](figs/rftrain.png)

### Prediction

![](figs/rfpredict.png)

# Boosting

## AdaBoost

![](figs/adaboost.png)

With learning rate $\alpha$:
![](figs/adaboostalpha.png)

## Gradient Boost

![](figs/gradboost.png)

With shrinkage: $y_{pred} = y_1 + \eta*r_1 + \cdots + \eta*r_N$ 
![](figs/gradboosteta.png)

## Stochastic Gradient Boosting

![](figs/stochasticgradboost.png)
