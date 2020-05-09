---
title: "Sorting"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```c++
#include <iostream>
#include <string>
using namespace std;
```

### Sort string


```c++
string str = "hgfedcba";
 string c_str(str);
 sort(c_str.begin(), c_str.end());
cout << c_str << endl;
```

    abcdefgh

