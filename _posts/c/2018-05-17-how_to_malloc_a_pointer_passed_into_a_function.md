---
header:
   image_fullwidth: "wallebanner.jpg"
layout: page
title:  "How to malloc() a pointer passed into a function."
breadcrumb: true
categories:
    - c
tags:
    - blog
    - content
    - post
      
---
<!--more-->

Here's how to pass a pointer to a function, `malloc()` some memory to the pointer, and access the `malloc()`ed memory after the function returns. 

```c
#include <stdio.h>
#include <stdlib.h>
void myFunc(char **ptr) {
     *ptr = malloc(100);
     printf("dereferenced ptr in myFunc(): %p\n", *ptr);
}
void main() {
     char *ptr = (char *)0x1234;
     myFunc(&ptr);
     printf("ptr after myFunc(): %p\n", ptr);
}
```

<h5>Output:</h5>
```c
dereferenced ptr in myFunc(): 0x55ed2fc29260
ptr after myFunc(): 0x55ed2fc29260
```

The _WRONG_ way: In this example, the pointer returned by `malloc()` is lost after `myFunc()` returns:

```c
#include <stdio.h>
#include <stdlib.h>
void myFunc(char *ptr) {
     ptr = malloc(100);
     printf("ptr in myFunc(): %p\n", ptr);
}
void main() {
     char *ptr = (char *)0x1234;
     myFunc(ptr);
     printf("ptr after myFunc(): %p\n", ptr);
     free(ptr);
}
```

<h5>Output:</h5>
```c
ptr in myFunc(): 0x55f536611260
ptr after myFunc(): 0x1234
```

This fails because:
* A pointer is just a variable holding a number (a memory address). It's like an int that holds a memory address.
* Passing a pointer to a function is like passing an int to a function. Any changes to the value stored in the variable won't last after the function ends.
* malloc() assigns a _new memory address_ to a pointer, thus changing the value stored in the pointer.

So, instead of passing a pointer (`ptr`) to `myFunc()`, we pass a pointer to a pointer (`&ptr`):

```c
char *ptr = (char *)0x1234;
myFunc(&ptr);
```

So before calling myFunc(), the picture might look something like this: (if the address of `ptr` arbitrarily happens to be `0x9a32`).

```c
        &ptr          --------->  ptr (stored at 0x9a32)
-------------------   | points    -------------------
| contains 0x9a32 |----   to      | contains 0x1234 |
-------------------               -------------------
```

Once we're in myFunc() the picture looks like this:

```c
        ptr           ---------> *ptr (stored at 0x9a32)
-------------------   | points    -------------------
| contains 0x9a32 |----   to      | contains 0x1234 |
-------------------               -------------------
```

We don't want to alter the value in `ptr (0x9a32)` because that was the value passed to `myFunc()` and any change to it will be lost when myFunc() ends.

So in myFunc() we dereference `ptr` with `*`:

```c
*ptr = malloc(100);
```

`malloc()` returns an address, say `0x5880` pointing to freshly allocated memory. Now the picture looks like this:

```c
        ptr           ---------> *ptr (stored at 0x9a32)
-------------------   | points    -------------------
| contains 0x9a32 |----   to      | contains 0x5880 |
-------------------               -------------------
                                          |
       (stored at 0x5880) **ptr <----------
       ------------------------
       | 100 bytes of freshly |
       | allocated memory     |
       ------------------------
```

Once `myFunc()` ends and we're back in `main()`, the picture (simplified) looks like this:

```c
        ptr                    ------------------------
-------------------  points to | 100 bytes of freshly |
| contains 0x5880 |----------> | allocated memory     |
-------------------            ------------------------
```