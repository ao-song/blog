---
title: Coroutine
date: 2019-11-08 21:06:23
tags: Programming
---

Implemented a coroutine library called [fiber](https://github.com/ao-song/fiber) in c utilizing ucontext today, coroutine mostly can be used in high IO scenarios.

This fiber library was implemented with stack-less fibers or called copy-stack fibers. Basically means each fiber does not have own stack but share the same one. Some ideas was borrowed from this [paper](http://akira.ruc.dk/~keld/research/COROUTINE/COROUTINE-1.0/DOC/COROUTINE_REPORT.pdf).

The code of store and restore stack is very interesting with the char x to define the latest position in stack.

> store
```
void Coroutine::StoreStack() {
    if (!Low) {
        if (!StackBottom)
            Error("StackBottom is not initialized");
        Low = High = StackBottom;
    }
    char X;
    if (&X > StackBottom)
        High = &X;
    else
        Low = &X;
    if (High - Low > BufferSize) {
        delete StackBuffer;
        BufferSize = High - Low;
        if (!(StackBuffer = new char[BufferSize]))
            Error("No more space available");
        }
        memcpy(StackBuffer, Low, High - Low);
    }
```

> restore
```
void Coroutine::RestoreStack() {
    char X;
    if (&X >= Low && &X <= High)
        RestoreStack();
    Current = this;
    memcpy(Low, StackBuffer, High - Low);
    longjmp(Current->Environment, 1);}
```