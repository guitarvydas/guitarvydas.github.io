---
layout: post
title:  "What Is A Program?"
---

From my perspective, a *computer* is a *machine* that can be used to augment human capabilities.

As such, we want to learn how to control such machines.

This leads to the question of "what is a programming language?". 

# What Is A Programming Language?

One view of a PL[^PL] is that it is a way to command the computer to do *what is needed*.

[^PL]: PL means Programming Language.  GPL means General Programming Language.

Another view might be that a PL is a way to command a computer to do what the *programmer thinks is needed*.

The former perspective involves the end-user (aka the customer).

The latter perspective does not involve the end-user directly[^1].

Question: Is a Programming Language intended only for programming nodes on a network, or, is a progamming language intended for programming the complete network (i.e. a language for networks)?

[^1]: Certain programmers understand the needs of end-users better than other programmers. I call such programmers "Software Architects".

# Calculators Are A Sub-Class Of Computers

One use of computers is to build calculators.

Input *something*, and always expect to receive a *result*.

This is less than what computers are capable of doing.

# Functions Are Calculators

- Functions are synchronous.
- Functions alway return some kind of result.
- Functions receive inputs in synchronous blocks (parameter lists).
- Functions produce results in synchronous blocks (return values and exceptions).
- *Calling a function* is a scheduling decision and overrides the Dispatcher(). (The caller schedules the callee to execute immediately. The caller suspends until a result has been produced).
- Functional notation does not include the notion of a component that does not return a result. [_This might be akin to the difference between Natural Numbers and Whole Numbers - 0_].

# Computers Contain State

Computers can contain state.  

For example, a server on a network might remember which client(s) it is producing responses for.

As such, computers are a superset of what is commonly called FP (functional programming).

FP is a useful notation for a portion of computing. 

# Computers Contain History - Computers Are Functions of Time

Computers can contain history.  

For example, a server on a network might remember which client(s) it is producing responses for and in which state each of those responses is.

As such, computers are a superset of what is commonly called FP (functional programming).

FP ignores the dimension of *time*.  It is *possible* to represent *time* in FP, but it is not inherent to the notation.

FP is a useful notation for a portion of computing. 

# Sequencing

Sequencing means function-of-time.

Music is a hard-realtime activity.

[_We teach this hard-realtime notation to 5-year-olds, yet, programmers continue to struggle with the concepts of realtime._]

## DAWs

DAWs (Digital Audio Workstations) control audio-generating computers in sequence.

## iMovie, OBS, DaVinci Resolve, Etc.

Video editors are like DAWs - they control and edit sequences of video (and audio) clips.

# 4D to 2D Mapping

I like to think of computers as dealing with 4D - x, y, z, t.

Textual progamming languages tend to map this 4D space to 2D space (`x,y,z,t` mapped to `x,y`).

Actually, textual GPLs tend to map 4D to 1½D.  X tends to represented as character offsets and Y tends to be represented as line numbers.  

In this kind of mapping, character cell are not allowed to overlap.

This perspective is a hold-over from paper-based typesetting.

Computers are capable of representing cells which overlap, but, most GPLs do not allow for this possibility.

# Complexity

This mapping makes progamming languages appear to be complicated.  

The choice of mappings can make some operations appear more complicated than others.

# Software Architecture

There are many ways to map 4 dimensions onto 2 dimensions.

Software Architecture is the act of *choosing* mappings.

# Multiple Notations

There are many ways to map 4 dimensions onto 2 dimensions.

Sticking to only one mapping results in accidental complexity.

Multiple notations should be used in every solution[^toy].

It is fruitless to pursue/explore the use of *only* one notation.

[^toy]: "Toy examples" lend themselves to a single mapping.

# Layers

A solution should be built in layers.

Each layer must be understandable in its entirety.

For example, the field of psychology determined that humans can understand 7±2 concepts at any one time. This implies that a *layer* should contain no more than 7±2 components / concepts (lines of code, components, functionalities, etc.)

A layered approach does not mean that details are ignored, it simply means that details are suppressed (elided) to lower layers.

Programming research should be expended on the issues of how to combine layers to produce final (otherwise-complicated) applications. Complicated applications should be broken down into a set of single, uncomplicated concepts. Corrolary: much research has been conducted on perfecting the notion of single programming languages, now, we need research on how to join (pipeline, overlay) such languages to produce applications. 

Question: How can developers overlay languages (like acetates used in original Disney cartoons)?

Question: How can developers plug software components together like LEGO® blocks[^2]?

## Scoping

Scoping is a layered approach applied to the problem of *global variables*.

Global variables are not a problem.  

Unrestrictd use of global variables is a problem.

Scoping is a layered approach to restricting the use of variables.

## Structured Programming

Structured Programming is a layered approach applied to the problem of unrestricted use of GOTOs.

GOTOs are not a problem.  

Unrestricted use of GOTOs is a problem.

Structured programming is a layered approach to restricting the use of GOTOs.

[^2]: Part of the answer is to make inter-component communication (e.g. messages) be of exactly only one, very simple, type.  Further types can be built up in layers. [_See the type stacks essay, below_]

# Servers Run Forever

Servers are built using the notion that they run forever / continuously.

It is considered to be a bug if a server stops working.

FP notation does not, inherently, include the concept of "run forever".  Functions spring to life, then die.

# Outdated Concepts

## Time-Sharing

Time-sharing was invented in the 1950's when CPUs were expensive.

Time-sharing leads to numerous forms of accidental complexity, e.g. preemption, thread safety, etc.

The ground rules have changed.  

CPUs are no longer expensive.

Yet, we continue to install time-sharing into most applications (for example, via thread libraries)

## Memory-Sharing

Memory-sharing was invented in the 1950's when memory was expensive.

Thread safety is an example of accidental complexity arising from the use of memory sharing.

The ground rules have changed. 

Memory is no longer expensive.

## Distributed Computing

The concepts of *distributed computing* (internet, blockchain, p2p, etc.) challenge the basic tenets of how software is currently constructed.

## Loops/Recursion

The concepts of loops and recursion are non-starters in distributed computing environments[^loops].

Loops/recursion should be the exception, not the norm, in new programming languages.

[^loops]: Networked components `Send()` messages to each other.  Loops can be constructed by `Send()`ing `do it again` messages to oneself. Loops (recursion) only make sense *inside* of network nodes, not over the network itself.

## Call/Return

Call/Return is a synchronization primitive.

Call/Return is a scheduling decision.

Call/Return is implemented - in hardware - using a global variable (SP - the stack pointer).

In *distributed computing* the concept of call/return does not exist.

[_Call/return can be used to program nodes in a network but does not inherently exist in distributed computing.  Programmers have stretched the synchronous metaphor to include RPC (remote procedure call), but this is not a fundamental concept of true distributed computing_.]

# FBP

FBP means Flow Based Programming.

Flow-based programming treats data as physical objects on a conveyor-belt.

Asynchronous components process data as it arrives (on the conveyor belts).

FBP component have input and output *ports*.

FBP components can *pull* and *push* data.

## Rust-Like Ownership

FBP uses *ownership*.  

# See Also

[Design Intent](https://guitarvydas.github.io/2021/04/11/DI.html)

[Type Stacks](https://guitarvydas.github.io/2020/12/09/Type-Stacks.html)

[Call/Return Spaghetti](https://guitarvydas.github.io/2020/12/09/CALL-RETURN-Spaghetti.html)

[Whole Numbers vs. Natural Numbers](https://www.cuemath.com/numbers/difference-between-natural-and-whole-numbers/])

[Flow Based Programming](https://en.wikipedia.org/wiki/Flow-based_programming)

[Blog](https://guitarvydas.github.io)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 