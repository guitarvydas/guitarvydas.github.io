---
layout: post
title:  "Software Components - A Language For Distributed Processing"
---
I discuss various issues regarding Software Components.

I would suggest browsing the table of contents instead of reading this document in a serial fashion.

- [Old](#old)
- [New](#new)
- [Optimization](#optimization)
- [Run Forever](#run-forever)
- [Single Thread](#single-thread)
- [Message Routing](#message-routing)
- [Visibility](#visibility)
- [Hierarchy](#hierarchy)
- [Layering](#layering)
- [Recursive Definition, Elision](#recursive-definition--elision)
- [Layered Components](#layered-components)
  * [Leaf Nodes - Bottom](#leaf-nodes---bottom)
  * [Compound Components - Composition](#compound-components---composition)
- [Compound or Leaf](#compound-or-leaf)
- [State](#state)
- [Isolation](#isolation)
- [Black Boxes](#black-boxes)
- [LEGO®-Like Pluggability](#lego--like-pluggability)
- [Pluggability API](#pluggability-api)
- [Transport layer](#transport-layer)
- [Tagged message](#tagged-message)
- [Referential Transparency](#referential-transparency)
- [Micro-Services](#micro-services)
- [Looping](#looping)
- [Dispatcher](#dispatcher)
- [Run To Completion, Finish Promptly](#run-to-completion--finish-promptly)
- [Memory sharing](#memory-sharing)
- [Time sharing](#time-sharing)
- [Preemption](#preemption)
- [Looping and Recursion](#looping-and-recursion)
- [See Also](#see-also)


# Old
- calculators
- loop/recursion
- stack
- synchronous operation
- always return a result

# New
- components
- ports
- asynchronous operation
- can consume inputs and produce nothing
- Looping/recursion not allowed.


# Optimization

Components should be as small as functions in present-day GPLs[^gpl].

[^gpl]: GPL means General purpose Programming Language.

# Run Forever

Components run forever by default.

(Think *servers*).

# Single Thread

Components each have a single thread of control.

An analogy would be to imagine a network of small computers connected together by thin wires.  Each computer performs some function. The system of connected computers forms an application.

Components communicate via message passing (*send()* messages to the parent, *send()* messages to children).

# Message Routing

The *parent* of a component decides how to route messages between its children.

For example, if a component wishes to send a message to its sibling, it sends the message to its parent, then the parent routes the message to the sibling.

# Visibility

Components cannot name ("see") their siblings.

Most GPLs allow explicit naming of callees.  This is not allowed in a component-based system.

# Hierarchy

Message passing fails if it is done in a "flat" manner.

Components must be arranged in a hierarchical manner and messages can only be sent "up" and "down" the hierarchy.

An analogy would be the scoping rules that fixed the global variable problem.

Hierarchy is scope.  Scope is hierarchy.

Analogy: most PCs used flat file systems until UNIX popularized the hierarchical arrangement of file systems.

Hierarchical components do for software what UNIX file systems did for operating systems.

# Layering
Components are connected strictly in layers.

A component can *send()* results to its paren.

A component can *send()* commands to its direct children.

Otherwise, there is no cross-talk - components cannot talk to (nor see) their peers.

# Recursive Definition, Elision

Components can be built from:

- other components
- leaf nodes.

Ports must support fan-out, to enable elision and layering.

# Layered Components
## Leaf Nodes - Bottom
FBP, no inherent structure, +state
Actors, no inherent structure, +state
FP and calculators, no inherent structure
Relational and miniKanren - no inherent structure.

[N.B it is _possible_ to organize programs in a hierarchical manner using the above systems, but this is not enforced.]

## Compound Components - Composition

All non-leaf components are composed of other components.

A component can contain a network of other components (leaf and compound components).

# Compound or Leaf

A component is either

- a compound component, or,
- a leaf component

# State

Components can contain *state*.

State is not a problem.  Unrestricted use of state is a problem.

# Isolation

Components are isolated from one another.

It is not possible to know how a component is implemented.

It is not possible to know if a component uses state or doesn't use state, except by observing its behavior from the outside.

For example: If a component contains a "memory leak", this will not affect other components.

# Black Boxes

Components are black boxes.

# LEGO®-Like Pluggability

Components can be plugged together like LEGO® pieces.

# Pluggability API

Components support a single API and exactly one type

- the *tagged message*

Note that this does not mean that more elaborate typing is impossible.  Components can be joined together in a pipeline of ever-more-detailed types.

# Transport layer

The single-type API is like a _transport layer_ in computer networks.

Messages can be *sent()* using the simple API, but their content is defined by higher levels (inside receiving components).

Note that UNIX® pipelines work this way.  The "transport layer" is a line of text. /bin/*sh can plumb commands together easily. The inner layers of commands define the structure contained in lines, e.g. fields, etc.

# Tagged message

A message consists of two portions:

1. Tag
2. Data.

The *tag* is (probably) an integer that that further defines a message.

The *data* is anything.

Analogy: *tags* are like *pins* on hardware ICs.  *Data* is like the signal received/sent by hardware ICs.

# Referential Transparency

Since components are black boxes, they can be substituted only if their pins match the component-to-be-replaced.

In hardware, this is called *pin-compatibility*. 

# Micro-Services

Components can act like servers.

# Looping

Components can send messages to themselves.

This allows creation of loops, but is not built into the underlying programming language.

[_Existing languages can be modified so that their compilers break each iteration of a loop._]

# Dispatcher

Only the _Dispatcher_ can invoke components.

Components do not have access to _call/return_[^inner call] at the inter-component level.

Components cannot directly affect dispatching of other components.

[^inner call]: Of course, components can still used call/return and recursion internally.  What happens inside of a component stays inside of the component.

# Run To Completion, Finish Promptly

Components must run to completion.

Components must finish "quickly".

This is similar to the use of mutual multitasking.

Mutual multitasking was discredited when it was used for building operating systems. 

Operating systems are apps with a special purpose.  

Most apps don't present the set of problems faced by operating system apps (e.g. time-sharing and memory-sharing are needed by operating systems, but not needed by most apps).

Preemptive multitasking is considered to be the exception, not the rule.

# Memory sharing

_Memory Sharing_ is a technique driven by early versions of computers, where memory was in short supply and expensive.

It has become apparent that memory sharing is loaded with difficulties.

Memory sharing, and _mutable state_, should only be used in situations that require it.

At present, most Operating Systems supply memory sharing primitives to every application, regardless of whether the applications need to use memory sharing.

I suggest that Operating Systems need to be fundamentally redesigned (or, better, discarded completely).

# Time sharing

_Time Sharing_ is a technique driven by early versions of computers, where CPU power was in short supply and expensive.

It has become apparent that time sharing is loaded with difficulties.

Time sharing should only be used in situations that require it.

At present, most Operating Systems supply time sharing primitives to every application, regardless of whether the applications need to use time sharing.

I suggest that Operating Systems need to be fundamentally redesigned (or, better, discarded completely).

# Preemption

Preemption is a epicycle added to operating systems.  Preemption is a brute-force technique that yanks the CPU out from under an application.

Preemption was added to operating systems because long running loops were thought to be essential.

Removing long-running loops (and deep recursion) would obviate the need for preemption.  Message-based systems could create loops by sending messages to themselves.

Preemption is built into most operating systems and becomes part of every application that uses the operating system(s).

Full preemption causes its own set of problems, commonly known as _accidental complexity_.

Full preemption is required by only a few applications, e.g. operating systems (Linux, Windows, MacOSX, etc.)

Early on, mutual multitasking was tried as an alternative to full preemption.  This technique was discredited for the wrong reasons - it was used to implement operating systems (the only kind of app that requires preemption) and failed to provide isolation between applications running under those operating systems.  Those applications did not "play well together", since they used long-running loops

Looping (and deep recursion) is an outdated concept.

_Infinite loops_ are application bugs like any other bug.

If apps were bug-free and did not contain long-running loops (or deep recursion), operating systems would not be needed.

One of the causes of needing loops in programs is that apps are treated as functions, instead of as a series of (small) steps.

We witness the demise of loops with the rise of distributed computing, e.g. internet, blockchain, etc.  The main contribution of the seminal [pBFT](http://pmg.csail.mit.edu/papers/osdi99.pdf) paper was to unroll functions into a series of steps that could be executed in a distributed network of computers[^fig1].

[^fig1]: Note that the pBFT technique was described in Fig. 1 of the paper as a diagram instead of as a function.

# Looping and Recursion

Many of the emerging GPLs do not provide Loops as an explicit concept. For example, GPLs based on FP and Relational concepts. In general, these kinds of GPLs provide Universal Quantification (forall), but do not provide explicit looping.

Looping and recursion are low-level implementation details.

# See Also
[The Algol Bottleneck](https://guitarvydas.github.io/2020/12/25/The-ALGOL-Bottleneck.html)
[Type Stacks](https://guitarvydas.github.io/2020/12/09/Type-Stacks.html)
[Blog](https://guitarvydas.github.io)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
