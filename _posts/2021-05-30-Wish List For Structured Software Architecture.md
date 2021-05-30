---
layout: post
title:  "Wish List for Structured Software Architecture"
---

# Wish List for Structured Software Architecture #

- scalability
- understandability - It is the Software Architect’s responsibility to make a design readable and understandable. 
- coordinated operation of multiple asynchronous processes

[DI](https://guitarvydas.github.io/2020/12/09/DI-Design-Intent.html).

[DI means Design Intent.]

# Scalability #

A Component is scalable if 
- it does not leak information, and,
- it has no dependencies.

A Component does not leak information if its data flows are explicit and constrained.

A Component does not leak control flow if it is fully [isolated](https://guitarvydas.github.io/2020/12/09/Isolation.html).[^oop]

[^oop]: Note that OOP provides encapsulation of data, but is not fully isolated, because it leaks control flow (inheritance, overriding of methods, specializatino of methods).  OTOH, UNIX processes, running with hardware MMUs, are fully isolated - one app cannot leak memory or control flow to another app (except through operating system traps).

# Strict Lines of Communication #

A Component can:
- receive commands from a parent
- send commands to children
- receive data from children
- send filtered data to parent.

Components are defined recursively.

## Lines of Communication ##

A Component can communicate (Send) to:
- its parent
- any of its direct children.

A Component can:
- receive commands from a parent
- send commands to children
- receive information from children
- send filtered informationto parent.

Component actions (message sending/receiving) are defined recursively.

A _command_ can contain information.

## Children ##

A Component can contain any number of children components.

Components that contain no children are called _links_.

### DI Hierarchy ###

DI means Design Intent.

To provide scalability, as defined above, the DI

- must be arranged in a tree hierarchy, and, 
- nodes in the hierarchy must only communicate only along edges of the tree.

The hierarchy must be a strict _tree_.

A Graph[^graph] cannot express a scalable architecture hierarchy, since graphs allow any node to be connected to any other node in a spaghetti-like manner.

A DAG cannot express a scalable architecture[^graph]. DAGs allow spaghetti connections.

[^graph]: Graphs and DAGs can be used to express the insides of nodes, but not a higher-level DI hierarchy.


### Structured Programming ###

_Structured Programming_ constrained control flow by prescribing
- 1 input (control flow - entry point)
- 1 output (control flow - exit point).


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
