---
title: "Which DataFrames merging should I use: append, concat, merge() and join()?"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
* `df1.append(df2)`: stacking vertically
* `pd.concat([df1, df2])`:
    - stacking many horizontally or vertically
    - simple inner/outer joins on Indexes 
* `df1.join(df2)`: inner/outer/left/right joins on Indexes
* `pd.merge([df1, df2])`: many joins on multiple columns

