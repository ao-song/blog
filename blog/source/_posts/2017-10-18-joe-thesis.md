---
title: Paper of Erlang
date: 2017-10-18 11:27:43
tags: Erlang
categories: Programming Language
---

这几天在读*Armstrong*关于*erlang*的博士论文，这里做一点笔记。

## Definition of an architecture
- A problem domain \- what type of problem is the architecture designed to solve?
- A philosophy \- reasoning behind the method of software construction, the central ideas in the architecture.
- A set of construction guidelines \- how to program and maintain the system following the underlying philosophy.
- A set of pre-defined components \- easier than design from scratch, like OTP.
- A way of describing things \- the interfaces to a component, a communication protocol between components, static and dynamic structure of the system.
- A way of configuring things \- how to start, stop, configure the system. re-configure in operation.

## Problem domain
The problem domain here is what erlang was initially designed for, actually a telecom system.
- **Concurrency** \- Be able to handle a very large numbers of concurrent activities.
- Soft real-time \- Actions must be performed at a certain point in time or within a certain time.
- **Distributed** \- System must be distributed over several computers.
- Hardware interaction \- The system is used to control hardware(eh..).
- Large software systems \- The software systems are very large.
- Complex functionality \- The system exhibits complex functionality such as feature interaction.
- **Continuous operation** \- The system should be in continuous operation for many years.
- **Hot upgrade** \- Software maintainance should be performed without stopping the system.
- **Quality requirements** \- Stringent quality and reliability requirements.
- **Fault tolerance** \- Fault toerance both to hardware failures and software errors must be provided.


