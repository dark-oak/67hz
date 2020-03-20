---
layout: post
title: g++ compiler flags you should know about
---


I decide to `Compile` a list of flags I've stumbled upon while grepping the compiler man pages - after all, who will compile the compilers?

This first one is great. Like most C++ devs, I am a huge fan of Scott Meyers ***Effective*** series of books. Any tech read that makes me laugh out loud deserves a permanent place on the bookshelf.

I love this tidbit from the Recommended Reading section of ***More Effective C++*** regarding James Coplien's ***Advanced C++ Programming Styles and Idioms***:

>>I generally refer to this as "the LSD book," because it is purple and it will expand your mind.
>>
>> Scott Meyers - More Effective C++


...Back to flags. I found this gem trying to remember how to disable copy elision (`-fno-elide-constructors`).

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


