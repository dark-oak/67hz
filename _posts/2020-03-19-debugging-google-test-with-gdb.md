---
layout: post
---

Debugging and unit testing should be logically inseparable. That being said, for those of you who are new to Google Test, this flag makes all the difference.

`--gtest_catch_exceptions=0`

It is in the docs, but not readily apparent. Hopefully, this saves y'all some time if you are wandering the docs aimlessly wondering how on earth you are going to break on that failing test that has you seeing red.

GDB's tab completion makes it easy to find the test you need. Just follow the format below. In the example, `bt` is issued in the offending test's function body to issue a backtrace. This accounts for about 90% of my gtest debugging workflow. Start with a backtrace and work backward or something to that effect.


```bash
$ gdb
(gdb) file <yourTestExecutable>
(gdb) setargs --gtest_catch_exceptions=0
(gdb) break <TestSuite>_<TestName>_Test::TestBody()
(gdb) r
(gdb) n
(gdb) bt
(gdb) ****gremlins****
```

Et voila!
