---
layout: post
title: compiler flags you should know about
category: software
---


I decide to `Compile` a list of flags I use or may have stumbled upon while grepping the compiler man pages trying to remember how to disable this or that - after all, who will compile the compilers?

# 1. The Meyers flag (g++)


This first one is great. Like most C++ devs, I am a huge fan of Scott Meyers ***Effective*** series of books. Any tech read that makes me laugh out loud deserves a permanent place on the bookshelf.

I love this tidbit from the Recommended Reading section of ***More Effective C++*** regarding James Coplien's ***Advanced C++ Programming Styles and Idioms***:

>>I generally refer to this as "the LSD book," because it is purple and it will expand your mind.
>> --<cite>Scott Meyers - More Effective C++</cite>


...But, back to flags.


```
-Weffc++
```

This give you some extra insight even compared to `-Wall`.

It is overly cautious so you will get flags on some of the standard library headers. If assignment happens within ctors, expect member initialization list warnings. For example, the following code will throw a warning:


```cpp
class SomeContainer {
private:
    double* elem;
    int sz = 0;

public:
    SomeContainer(int s) {    // warns about lack of member init list
        if (s < 0) // but a class invariant is useful in this case
          throw length_error("Container constructor: negative size");
        elem = new double[s];
        sz = s;
    }
}
```

See `man g++` for details...


```
-Weffc++ (C++ and Objective-C++ only)
   Warn about violations of the following style guidelines from Scott
   Meyers' Effective C++ series of books:

   *   Define a copy constructor and an assignment operator for classes
       with dynamically-allocated memory.

   *   Prefer initialization to assignment in constructors.

   *   Have "operator=" return a reference to *this.

   *   Don't try to return a reference when you must return an object.

   *   Distinguish between prefix and postfix forms of increment and
       decrement operators.

   *   Never overload "&&", "||", or ",".

   This option also enables -Wnon-virtual-dtor, which is also one of the
   effective C++ recommendations.  However, the check is extended to warn
   about the lack of virtual destructor in accessible non-polymorphic
   bases classes too.

   When selecting this option, be aware that the standard library headers
   do not obey all of these guidelines; use grep -v to filter out those
   warnings.

```

# 2. Disable copy elision 



Modern C++ gives us move semantics for free. No more worrying about returning that 
million member container by value. But, sometimes it can be "fun" to see what could have been. 

`-fnoelide-constructors`

Set this flag and watch your copy ctors light up. No more copy elision. I actually find this one to be useful as a reminder to implement move ops.






