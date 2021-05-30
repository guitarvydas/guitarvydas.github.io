---
layout: post
title:  "Operating Sytems in One Page"
---

# Operating System - Windows, MacOS, Linux, etc.

Most operating systems are composed of millions of lines of code.

How can the _essence_ of each of these operating systems be captured in only one page of code?

# One Page
## Keeping Details
We want to keep _all_ of the details.

But, [details kill](https://guitarvydas.github.io/2021/03/17/Details-Kill.html).

Q: How do we keep the details while minimizing the complexity? 

(You already know the answer :-).

## Decomposing Complexity
We must _decompose_ complexity.

We must _decompose_ complexity into layers.

Using _hierarchy_ allows us to show details in layers.

Using _components_ allows us to show details in `hierarchical layers`.

The concept of components are already be familiar to most people.

The only _new_ idea here is the obersavation of psychology and how it affects our designs.

If we use a PL[^pl] that gives us only one layer, then we will tend to design everything in one layer.

Most PLs _allow_ hierarchical decomposition, but do not _encourage_ it.

[pl]: PL means Programming Language.

### Components

What is a `Component`?

A Component is a black box.

We can characterize components as below:
- input commands from parent
- input information from children
- filter information and `Send ()` filtered information to Parent

The points of Components are:
- no inter-component dependencies
- reducing information flow, instead of using an all-in-one mind-set. 

Well-designed Components use no side-channels.

Well-designed Components, make all dependencies explicit (e.g. Parent/Children relationships).

## Concurrency
Components are easier to design and use in the concurrent paradigm.

The _synchronous_ paradigm makes it harder to think of components and to use them. We resort to complicated structures, like code libraries, dependency managers

_Asynchrony_ is easy - if you don't try to express it in the _synchronous_ paradigm.

Multitasking, as we know it, is accidental complexity created by expressing _asynchrony_ in a _synchronous_ paradigm and on _synchronous_ hardware[^hw].

_Synchronous_ design is a good paradigm for designing calculators.

_Synchronous_ design is not a good paradigm for designing distributed systems[^sync].

[^sync]: Currently, we resort to using low-level concepts, like thread libraries, to implement distributed systems as multiple envelopes containing exactly one calculator each.  This is what assembler programmers did while resisting the use of HLLs.

[^hw]: CPUs were OK until they added The Stack (a global variable).  IBM 360s did not have Stacks built into the hardware - programmers had to use BALR instructions if they really, really wanted control-flow stacks.  BALR did not constrain programmers to using a global variable, programmers could build stacks in the heap, if they wanted to.  Today, all stacks are in shared memory and we have to resort to accidental complexities like multitasking and full preemption.

## Dependencies
We _want_ software components that have _no_ dependencies between them.

We can't scale systems that have inter-component depedencies.

Q: How can we build components that have no dependencies?

### Docker

Docker is a symptom of systems that have dependencies.

We use _docker_ instead of fixing the problem - the Elephant in the Room.

### Make

_Make_ allows us to cope with dependencies.

We use _make_ instead of fixing the problem - the Elephant in the Room.

### Package Managers

Dependency Managers, like _npm_, allow us to cope with dependencies.

We use dependency managers instead of fixing the problem - the Elephant in the Room.

## Can Types be Componentized?

Q: Can Types be Componentized?

A: Yes.

For example:
```
bit -> byte -> word -> ... -> mid-level abstractions -> high level abstractions
```

See [type stacks](https://guitarvydas.github.io/2020/12/09/Type-Stacks.html).

Q: How many levels of abstraction are there?

A: It depends.

We should build layers of abtraction that make sense for a given solution. Note the use of the word `solution`, and the avoidance on using the word PL.

### Hierarchical Types
	Decompose Types as Components 
	bytes vs. high-level constructs
### Hierarchical Functions	
### Hierarchical Variable Names
## Features
## File System
## Drivers
## Multitasking
### Time-Sharing
### Full Preemption
### Memory Sharing



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
