---
header:
   image_fullwidth: "wallebanner.jpg"
layout: page
title:  "How to create a custom C++ exception"
teaser: "Just the facts, ma'am."
breadcrumb: true
categories:
    - c++
tags:
    - blog
    - content
    - post
      
---
<!--more-->

Create a header file with the same name as your exception like so:
<br>
<h5>gcryptinitexception.h</h5>
```c++
#ifndef GCRYPTINITEXCEPTION_H
#define GCRYPTINITEXCEPTION_H

class GcryptInitException: public std::exception {

public:
    GcryptInitException() {}

    virtual const char* what() const throw() {
        return "Couldn't initialize gcrypt.";
    }
};

#endif // GCRYPTINITEXCEPTION_H
```

Then `#include` your header file and throw it like this:<br><br>`throw GcryptInitException();`<br><br>(Don't forget the parenthesis at the end)