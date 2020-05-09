---
title: "Function arguments, by reference"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```c++
#include <iostream>
using namespace std;
```

### Pass by pointer

Pass-by-pointer means to pass a pointer argument in the calling function to the corresponding formal parameter of the called function. The called function can modify the value of the variable to which the pointer argument points
Pass by pointer using a pointer, here you can pass a `NULL` pointer


```c++
double f1(double* x, double* y)
{
    std::cout << "val x: " << *x << "\n";
    std::cout << "val y: " << *y << "\n";
    return *x * *y;
}
```


```c++
void swapnum_byPointer(int *i, int *j) {
  int temp = *i;
  *i = *j;
  *j = temp;
}
```


```c++
{int a = 10;
int b = 20;
swapnum_byPointer(&a, &b);
cout << "A is " << a << " and B is " << b << endl;
}
```

    A is 20 and B is 10


### Pass by reference

Pass by reference by creating an alias to the arguments you pass. Use `const` to not change these arguments


```c++
double f2(double const &x, double const &y)
{
    std::cout << "val x: " << x << "\n";
    std::cout << "val y: " << y << "\n";
    return x * y;
}
```

Pass by reference by creating an alias to the arguments you pass. Do not use `const` if you plan to modify the arguments


```c++
double f3(double &x, double &y)
{
    std::cout << "val x: " << x << "\n";
    std::cout << "val y: " << y << "\n";
    return x * y;
}
```


```c++
{double a, b;
a = 2;
b = 3; 
std::cout << f1(&a, &b) << "\n";
std::cout << f2(a, b) << "\n";
std::cout << f3(a, b) << "\n";
}
```

    val x: 2
    val y: 3
    6
    val x: 2
    val y: 3
    6
    val x: 2
    val y: 3
    6



```c++
void swapnum(int &i, int &j) {
  int temp = i;
  i = j;
  j = temp;
}
```


```c++
{int a = 10;
int b = 20;
swapnum(a, b);
cout << "A is " << a << " and B is " << b << endl;
}
```

    A is 20 and B is 10



```c++
void modify_const(const int& x) {
  int& y = const_cast<int&>(x);
  ++y;
}
```


```c++
{int a = 5;
  modify_const(a);
  cout << a << endl;}
```

    6


### Pass by value
The value of an argument is copied to a non-pointer or non-reference parameter in the called function definition. The parameter in the called function is initialized with the value of the passed argument. As long as the parameter has not been declared as constant, the value of the parameter can be changed, but the changes are only performed within the scope of the called function only; they have no effect on the value of the argument in the calling function.   

Pass-by-reference is more efficient than pass-by-value, because it does not copy the arguments.


```c++
double f4(double x, double y)
{
    std::cout << "val x: " << x << "\n";
    std::cout << "val y: " << y << "\n";
    return x * y;
}
```

#### Result


```c++
{double a, b;
a = 2;
b = 3; 
std::cout << f4(a, b) << "\n";
}
```

    val x: 2
    val y: 3
    6



```c++

```
