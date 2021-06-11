---
layout: post
title:  "CALL Violates Structured Programming"
---

Structured Programming introduced the notion of _nesting_ control flow with constructs like _if-then-else_, _while_, etc.

Object-Oriented Programming popularized the notion of _nesting_ data via inhertiance.

OOP and Structure Programming do not fully _isolate_ control-flow. `CALL / RETURN` is usually supported in hardware by a global variable (the Stack).

`CALL / RETURN` violates the single-entry-single-exit edict of Structured Programming. Programmers can CALL subroutines directly and "break through" the boundaries of a properly structured 

To enable software construction using components, we must fully _isolate_ data _and_ control-flow.

# Threads for Isolation of Control Flow
Threads, common in desktop operating systems like Linux, MacOS and Windows, isolate control flow in a heavy-handed manner. Threads often employ full-preemption and hardware MMUs.

Full preemption has caused a great deal of accidental complexity, e.g. the Mars Rover disaster.

Fixes for known problems have been developed, but it is clear that _full preemption_ inhibits reasoning about designs.
# Pure Functions for Isolation of Control Flow
FP restricts programs by expunging mutability to achieve _isolation_.

These kinds of languages severely restrict the programming paradigm(s) that can be employed to solve practical problems.


## Calculators - One Input One Output
FP makes it easy to treat computers as _calculators_.

FP assumes that all _functions_ have one block of inputs and one block of outputs.

FP is not well-suited to solving problems using paradigms that exceed this simple model. 

### Exceptions
For example, _exceptions_ are usually treated as edge-cases with second-class syntax and second-class semantics.

### Javascript
Javascript was invented for creating distributed programs (aka web pages).

Javascript continues to use function-like syntax with the result that simple distributed operations need to be programmed as _callbacks_.

## Referential Transparency

An ideal for component-based design is the ability to replace components with pin-compatible ones.

In hardware design, this was called _pin compatibility_.

In functional progamming languages, this is called _referential transparency_.

FP languages achieve _referential transparency_ by restricting the language paradigm that can be used. 

FP expunges mutability and mutable operations.

(Note that this is *not* the only way to achieve _referential transparency_. A different solution was developed in the electronics industry in the 1950's).
# Hidden Dependencies - Global Variables
A major factor in the complexity of computer systems is the hidden dependencies between modules and the hardware-supported used of a global Stack.

Earlier computers, e.g. the IBM 360, did not have a hardware-supported Stack (programmers had to simulate a Stack using the BALR instruction).

# Hidden Dependencies - Synchrony vs. Asynchrony
Most languages use a sequential function paradigm.  

This sequential model resists the natural paradigm for computing - asynchronous operation.

It should be noted that asynchrony is common in human experience
1. the human body contains an autonomous nervous system which consists of some 500 independent units
2. children around the age of 5 learn to use a hard, real-time notation
3. businesses run in a top-down manner (aka Org Charts) and consist of many independent units.

# Concurrency

--- spaghetti
--- The Stack
--- Scalability
--- Superposition

# See Also

[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
