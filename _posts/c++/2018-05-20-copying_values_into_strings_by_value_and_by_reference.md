---
header:
   image_fullwidth: "wallebanner.jpg"
layout: page
title:  "Assigning char arrays to C++ strings by value and by reference"
teaser: "Some experiments to see what happens when assigning char arrays to a string using a few different methods."
breadcrumb: true
categories:
    - c++
tags:
    - blog
    - content
    - post
      
---
<!--more-->

* using '=' to assign a char array to a string makes a _COPY_ of the char array.
* assigning a char array to a string with `string::assign()` does _NOT_ copy the char array.
* assigning a char array to a string in the string's constructor does _NOT_ copy the char array.

```cpp
#include <iostream>
using namespace std;
int main() {

  char myCharArray[] = "123";
  
  string myString = myCharArray;
  myCharArray[0] = 'A';
  cout << myString << endl; //123

  string myString2;
  myString2.assign(myCharArray);
  myCharArray[0] = 'B';
  cout << myString2 << endl; //A23
  
  string myString3(myCharArray);
  myCharArray[0] = 'C';
  cout << myString3 << endl; //B23

}
```

returns:
```cpp
123
A23
B23
```