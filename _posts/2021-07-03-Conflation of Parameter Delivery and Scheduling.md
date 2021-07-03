---
layout: post
title:  "Conflation of Parameter Delivery and Scheduling"
---

What does the following line of code do?
```
fn(a)
```
It:
1. Delivers the parameter "a" to the function _fn_, and, it
2. Schedules the function _fn_.


What does the following line of code do?
```
fn(a,b)
```
It:
1. Delivers _two_ parameters to _fn_ - both, at the _same time_, and, it
2. Schedules the function _fn_.
```

# Scheduling

Normally, we use an operating system to determine scheduling, but, in the case of a function CALL, we override the operating system.

If the operating system really, really, really wants to override the override, it resorts to preemption and yanks the CPU out from under the CALLer.

# Simultaneous Parameter Delivery

Is it true that we _always_ want to deliver parameters all-at-once?

That works when building calculators, but doesn't work so well when building internet software.

Most of the popular GPLs (general purpose language) make it easy to build calculators, but don't make it easy to build internet software. 

Yes, it is _possible_ to internet software using calculator languages, but it could be easier.

# ASCs - Asynchronous Software Components

It is possible to build languages tuned for building asynchronous applications.

I think we need to think about:
1. Asynchronous operation.
2. Components that run forever.
3. Sending Messages.
4. Structuring designs using hierarchy.
5. Relativity.

## Relativity
Components can only reference (call, query, etc.) components that are "nearby". UNIX gives us a notation for this "./hello", "../world", etc.
## Scalability
Any component that is tangled up with another component is _dependent_ on the other component and is, therefore, not scalable on its own.

Humanity has solved this problem before.  The most obvious example is the hierarchical organization of businesses. Humanity has even invented a phrase for non-scalability, e.g. "Going Over the Boss's Head"
## Asynchronous Operation
Humanity has invented notations for asynchronous operations and teaches this notation to 5-year old kids. 

Humanity calls this notation _sheet music_.

The notation is hard-real-time.

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
