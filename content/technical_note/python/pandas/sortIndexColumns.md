---
title: "Sorting DataFrame with Index & columns"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
months = ['Apr', 'Jul', 'Jan', 'Oct']
temp = [61.956044, 68.934783, 32.133333, 43.434783]
mytemp = {'Mean TemperatureF': temp}
weather1 = pd.DataFrame(mytemp)
weather1.index=months
print(weather1)

# Sort the index of weather1 in alphabetical order: weather2
weather2 = weather1.sort_index()

# Print the head of weather2
print(weather2.head())

# Sort the index of weather1 in reverse alphabetical order: weather3
weather3 = weather1.sort_index(ascending=False)

# Print the head of weather3
print(weather3.head())


# Sort weather1 numerically using the values of 'Max TemperatureF': weather4
weather4 = weather1.sort_values('Mean TemperatureF')

# Print the head of weather4
print(weather4.head())
```

         Mean TemperatureF
    Apr          61.956044
    Jul          68.934783
    Jan          32.133333
    Oct          43.434783
         Mean TemperatureF
    Apr          61.956044
    Jan          32.133333
    Jul          68.934783
    Oct          43.434783
         Mean TemperatureF
    Oct          43.434783
    Jul          68.934783
    Jan          32.133333
    Apr          61.956044
         Mean TemperatureF
    Jan          32.133333
    Oct          43.434783
    Apr          61.956044
    Jul          68.934783

