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

<!-- more -->

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

## Philosophy in brief
- A hierarchy of tasks -> strong encapsulation method, strong encapsulation for error isolation -> isolated processes -> concurrent programs
- Language process over OS process -> OSs irrelevant, much lighter-weight than OS process, easy to port to specialised environments like embedded systems.
- Applications structured using large numbers of communicating parallel processes -> provides an architectural infrastructure, potential efficiency, **fault isolation**.

**In generall, the essential thing is that to build large reliable systems by partitioning the system into independent parallel processes, and by providing mechanisms for monitoring and restarting these processes.**

## Concurrency oriented programming

### Programming by observing the real world
- Identify all the truly concurrent activities.
- Identify all message channels between the activities.
- Write down all the messages which can flow in the channels.

### Properties of COPL(Concurrency Oriented Programming Language)
- COPLs must support processes. A process can be considered as a self-contained virtual machine.
- Processes must be strongly isolated.
- Each process must be identified by a unique ID.
- There should be no shared state between processes.
- Message passing is assumed to be unreliable.
- It should be possible for one process to detect failure in another process.

### Process isolation
- Processes have "share nothing" semantics.
- Message passing is the only way to pass data between processes.
- Message passing is asynchronous.
- Since nothing is shared, everything necessary to perform a distributed computation must be copied.

### Names of processes
- Impossible to guess the name of a process.
- Process should know its name.
- A parent process knows the names of its children.

Knowing the name of a process is the key element of security.

### Message passing
- Atomic, either delivered in its entirety or not at all.
- Message passing between processes should be ordered.
- Message should only contain constants and/or PIDs.

## Essential requirements
Concurrency, Error encapsulation, Fault detection, Fault identification, Code upgrade, Stable storage.

## Erlang view of the world
- Everything is a process.
- Processes are strongly isolated.
- Process creation and destruction are lightweight.
- Message passing is the only way for processes to interact.
- Processes have unique names.
- If you know the name of a process you can send it a message.
- Processes share no resources.
- Error handling is non-local.
- Processes do what they are supposed to do or fail.

## Erlang error handling philosophy
- Let some other process do the error recovery.
- Let it crash, if you don't know how to handle the error in some situations, equally, do not program defensively, like case clause.

## Programming fault-tolerace
*If we cannot do what we want to do, then try to do something simpler.*

### Supervision hierarchies
- Supervision trees are trees of supervisors.
- Supervisors monitor(start/stop/restart) workers and supervisors.
- Workers are instances of behaviours.
- Behaviours are parameterised by well-behaved functions.
- Well-behaved functions raise exceptions when errors occur.

### Well-behaved functions
- The program should be isomorphic to the specification.
- If the specification doesn’t say what to do raise an exception.
- If the generated exceptions do not contain enough information to be able to isolate the error, then add additional helpful information to the exception.
- Turn non-functional requirements into assertions (invariants) that can be checked at run-time. If the assertion is broken then raise an exception.
