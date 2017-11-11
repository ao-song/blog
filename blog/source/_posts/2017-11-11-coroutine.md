---
title: Coroutine
date: 2017-11-11 19:37:44
tags: C
categories: Programming Language
---

Sometimes it is expensive for threads switch, coroutine could be used to make full use of time slots in one thread.

# yield function with switch...case

```c
int function(void) {
  static int i, state = 0;
  switch (state) {
    case 0: /* start of function */
    for (i = 0; i < 10; i++) {
      state = __LINE__ + 2; /* so we will come back to "case __LINE__" */
      return i;
      case __LINE__:; /* resume control straight after the return */
    }
  }
}
```

Ref: [Coroutines in C](https://www.chiark.greenend.org.uk/~sgtatham/coroutines.html)

# setjmp + longjmp
# ucontext
