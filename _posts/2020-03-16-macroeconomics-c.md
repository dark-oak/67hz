---
layout: post
title: macroeconomics in C
category: software
---


You cannot have C code without macros. Period. One of the biggest shifts moving to C++ from C is letting the preprocessor take a back seat. Ya, it still has its place, but not like in C.

This one is ubiquitous in systems programming:

```c
#ifndef BUF_SIZE  /* Allow "cc -D" to override definition */
#define BUF_SIZE 1024
#endif
...
char buf[BUF_SIZE];
```

The above example utilizes the hot-swap nature of predefined macros to give us a constant without the overhead of memory allocation. I had to re-program myself to stop doing this in C++ codebases. C++ is all about const correctness and what better place to have a const that something like in the example below.

```cpp
const size_t BuffSize = 1024;
char buf[BuffSize];
```

Of course there are a myriad of superior alternatives for array allocation in C++, not to mention the `std::array` class or better yet `std::vector`. But, I digress... Macros...


Glib is one of the most common libs in C. You get data structures, algorithms, and GObject for all your OOP needs. But, macros - Sweet Mary-Josephine are there some macros. Just look at a sampling of [Glib](https://developer.gnome.org/glib/stable/glib-Miscellaneous-Macros.html). This is just a list of ***miscellaneous macros***.

When defining custom `GObjects` there are convenience macros that leverage nested macros (i.e., **my macros have macros**). I have to keep `jumping to definition` just to remember what exactly is going on under these macros I am sprinkling all over my code. The convenience of macros expanding to generate class-like properties is no doubt awesome, but, hell... I need a giant cheat-sheet just to keep my ducks in a row.


On a separate non-rant, one of the lesser utilized features in C macros is the octothorp `#` as an eval tool. It's not just for `#define`s anymore.

Check this out. Here we are going to do 2 things: print the passed in macro param and then evaluate said param.


```c
#define Peval(cmd) printf(#cmd ": %g\n", cmd);

int main (int argc, char **argv)
{
    double list[] = {1,2,3};
    Peval(sizeof(list)/(sizeof(double)+0.0));

}
```
running this will output both the string to be evaluated and the evaluated string. Ya, I had to double-take that last sentence too. Trust me, it checks out.
```bash
    // program output
    sizeof(list)/(sizeof(double)+0.0): 3
```

