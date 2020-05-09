---
title: "++*ptr vs. *ptr++"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```c++
#include <iostream>
using namespace std;
```

### Rules
Prefix operator `++` has the same precedence as dereference: `++*ptr` = `++(*ptr)`. `++ptr` evaluates to the *incremented* value of `ptr`   
Postfix operator `++` has a higher precedence than dereference: So `*ptr++` gets evaluated as `*(ptr++)`. `ptr++` evaluates to the current value of `ptr`


```c++
{int x = 19;
int *ptr = &x;
cout << *ptr << endl;
cout << ++(*ptr) << endl;
cout << *ptr << endl;
 }
```

    19
    20
    20



```c++
{int x = 19;
int *ptr = &x;
cout << *ptr << endl;
cout << (*ptr)++ << endl; // *ptr++ means *(ptr++) and will give garbage
cout << *ptr << endl;
 }
```

    19
    19
    20

