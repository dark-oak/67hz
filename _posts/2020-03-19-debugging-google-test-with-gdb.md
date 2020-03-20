---
layout: post
author: Aaron
---

Debugging and unit testing should be logically inseparable. That being said, for those of you who are new to Google Test, here is a flag that makes all the difference in backtracing. `--gtest_catch_exceptions=0`. It's in the docs, but not readily apparent. Hopefully, this saves y'all some time if you are wondering how to break on a failing test.

GDB's tab completion makes it easy to find the test you need. Just follow the format below.

Below, we step into the source once we get to the failing test body and then issue a backtrace.

```bash
$ gdb
(gdb) file <yourTestExecutable>
(gdb) setargs --gtest_catch_exceptions=0
(gdb) break <TestSuite>_<TestName>_Test::TestBody()
(gdb) r
(gdb) n
(gdb) bt
```

Et voila!
