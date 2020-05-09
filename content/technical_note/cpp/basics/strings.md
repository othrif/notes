---
title: "Bitwise Operations"
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

### String size


```c++
{
string str = "hello";
cout << "String size is " << str.length() << endl;
}
```

    String size is 5


### String append

For one character, use `pash_back()` otherwise `append()`


```c++
{
string inStr = "123"; 
string outStr = ""; 
outStr.append("4"); 
outStr.append(inStr);
char x = 'X';
outStr.push_back(x); // Valid when appending 1 char
cout << outStr << endl;
}
```

    4123X


### String check space


```c++
{string str = " HEY ";
 
 for(size_t i = 0; i<str.length(); i++){
     if( isspace(str[i]) )
         cout << "Found space!" << endl;
     else
         cout << "Space Not found!" << endl;
 }
}
```

    Found space!
    Space Not found!
    Space Not found!
    Space Not found!
    Found space!



```c++
{string str = " ";
if(str == " ")
    cout << "Found!" << endl;
 else
     cout << "Not found!" << endl;
}
```

    Found!


### Erase a string


```c++
{
    string str ("This is an example sentence.");
    str.erase (str.begin()+5, str.end()-9);
    cout << str << endl;
}
```

    This sentence.


### Copy string to char array


```c++
#include <iostream>
#include <string>
#include <cstring>
using namespace std;
```


```c++
{std::string s = "Hello World!";

char cstr[s.size() + 1]; // +1 for /0 character
strcpy(cstr, s.c_str()); // or pass &s[0]

std::cout << cstr << '\n';
}
```

    Hello World!


alternatively, if you will not remember `strcpy`:


```c++
{
    std::string s = "Hello World!";
    char cstr[s.size() + 1]; // +1 for /0 character
    for (int i=0; i<s.size(); i++)
        cstr[i] = s[i];
    std::cout << cstr << '\n';
    
}
```

    Hello World!



```c++

```
