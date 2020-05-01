---
title: "Iterate over vector or array"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```c++
#include <iostream>
#include <vector>
```

# Iterate over std::vector


```c++
std::vector<float> v = {7.3, 5.1, 16.3, 8.9}; // T = int, it can be anything else
```

### Using iterators


```c++

for(std::vector<float>::iterator it = v.begin(); it != v.end(); ++it) {
    std::cout << *it << " "; /* ... */
}
```

    7.3 5.1 16.3 8.9 

### Using indices


```c++
for(std::vector<int>::size_type i = 0; i != v.size(); i++) {
    std::cout << v[i] << " "; /* ... */
}
```

    7.3 5.1 16.3 8.9 

### Using range


```c++
for(auto const& value: v) {
     std::cout << value << " "; /* ... */
}
```

    7.3 5.1 16.3 8.9 

# Iterate over arrays


```c++
double a[] = {7.3, 5.1, 16.3, 8.9, 9.1}; // T = int, it can be anything else
```

### Using indices


```c++
for(std::size_t i = 0; i != (sizeof a / sizeof *a); i++) {
    std::cout << a[i] << " "; /* ... */
}
```

    7.3 5.1 16.3 8.9 9.1 

### Using range


```c++
for(auto const& value: a) {
     std::cout << value << " "; /* ... */
}
```

    7.3 5.1 16.3 8.9 9.1 


```c++

```
