---
layout: post
title:  "Flows (Abridged)"
---

Computer software deals with two kinds of information:
1. data
2. control.

# Issues
## Separation of Concerns
See S/SL (in References) for an example of a data-less language.

## Locality of Reference
Information leaks are currently called "dependencies"[^locality].

An insidious form of information leak is the use of _functions_! 

# Scoping (Nesting)

In computer science, it has often been the case that problems have been solved through the use of nesting - aka _scoping_.

## Structured Programming

Structured programming prescribes _nesting_ of control-flow as a solution to the problem of _spaghetti_ control-flow.

## Global Variables

The problem of _global variables_ was solved using _nesting_.

The "real" problem is one of _spaghetti dependencies_.  How to stop programs from becoming "too large"? 

## Object Oriented Programming

OOP is a solution for structuring data and divorcing data from implementation details.

_Inheritance_ is a useful way to organize data.

_Inheritance_ is a poor way to organize code.

## Syntax

Syntax is, currently, used for dealing with control-flow descriptions. 

Two languages for any program - 

1. a data description language
2. a control-flow description language

## Pattern Matching
The trend in FP is to use _pattern matching_ to separate control information from data information.

Pattern matching is well-understood, albeit under a different name - "parsing".

## Denotational Semantics

Denotational Semantics is the field of describing programming languages using functional notation.

Control-flow, in Denotational Semantics, is most often handled through the use of `GOTOs` (rebranded as CPS, first-class-functions, continuations, etc.).

## Data Flow

"Data flow" refers to a style of control-flow, not to data structuring.

FP requires that _all_ inputs arrive at a component (a _function_) at the same time.  FP assumes that there is a single _happy path_.

## Control Flow

The current model for control-flow - syntax - is based on assumptions related to 1950's computer hardware - e.g. a single CPU[^cpu] and expensive memory.

## Deep Recursion, Long-Running Loops

## State

Programmers conflate the various uses of _state_ and lump them together.

I discuss this further in https://guitarvydas.github.io/2021/03/30/State,-Analysis-of.html. 

## StateCharts

I discuss StateCharts further in https://guitarvydas.github.io/2020/12/09/StateCharts.html and https://guitarvydas.github.io/2021/02/25/statecharts-(again).html.

Note that many "successes" in programming have been built on top of the _state_ paradigm, e.g. operating systems, YACC, LEX, REGEXP, etc.

## Threads

_Threads_ are more like assembly-level operations provided on a single CPU than a high-level concept useful for programming distributed systems.

## Dataless

See the References section for S/SL - a dataless language that was, ostensibly, used for constructing compilers (aka "big" programs).

## GOTOs, CPS

The problem with GOTOs was not the GOTOs themselves, but the unstructured use of GOTOs.

## Scalability

Components are scalable only if they are not inter-related.

Scalable components cannot have dependencies on one another.

https://guitarvydas.github.io/2021/06/17/Dags.html

## Type Checking

Currently, most PLs provide a handful of hard-wired types and a way for programmers to define further types. 

### Hard-Wired

### Programmer-Defined

### Input Validation

### Tell

The fact that three forms of type checking exist is a _tell_ that the concepts of type checking are non-uniform.

## Absolute Naming

Most PLs create names that are _absolute_ and global to the whole application.

# Solutions

## Dependencies

At present, I believe that dependencies are the first-order problem.

... _dependency debt_.

### Visualizing Dependencies

I believe that diagrams show dependencies more readily than textual code.

## Little Things

The Little Things matter.

https://guitarvydas.github.io/2021/04/26/What-If-Making-A-Compiler-Was-Easy.html

## Asynchronous Components

Software components are _asynchronous_ by default.

Synchronous components are the exception, not the rule.

### Lifetimes

Software components "live forever" (like web servers).

### Parameters

Software components can be supplied inputs at different points in their lifetimes.

### Outcomes

Software components can produce outputs at various points in their lifetimes.

### Exceptions

Exceptions are not exceptional.

Exceptions produced by components are the same as all other outcomes produced by components.

The problems and the solutions dictate which outcomes are considered to be erroneous.  _Software Architects_ design solutions that produce the desired outcomes, picking from a multitude of choices.  Few problems have exactly one solution - it is the Architects' responsibility to make vaarious trade-offs and to make the design clear to readers.

https://guitarvydas.github.io/2020/12/09/DI-Design-Intent.html

## Ports

Software components have input _and_ output ports.

Most current PLs have APIs that imply synchronous operation.

### One Universal Type

Components are plugged together port-to-port where ports have a _single_, universal, simple type, e.g. a _message_.

Types checking is done in a pipeline, from simple to more complex.  

Not _all_ software components need to fit this simple - one-in-two-out - model.

## Layering

Components are built in layers.

No layer contains more units than can be comprehended, e.g. 7±2.

Components can, themselves, contain layers, recursively.

##  Loops

Long running loops and deep recursion are not allowed.

## Diagrams

Diagrams are a way to visualize multiple outcomes.

Diagrams are a way to show nesting and locality of reference.

Diagrams can visualize information leakage.

Diagrams make it difficult to draw leaky components, especially when _everything_ (e.g. function calls) is made explicit.

### Example Diagram Scenario

A software component is represented as a box.

Software components are asynchronous.

Lines represent message flow paths.

Software components contain input and output ports.

Input ports are small green circles.

Output ports are small yellow circles.

A Dispatcher routine invokes _ready_ components in a random order.

## Relative Naming

All names are relative to components.

### Namespaces

Components have 5 namespaces:

1. inputs

2. ouputs

3. contained components

4. connections between components

5. other

### Example

A component refers to a component that is contained in it by using a name (e.g. "inner") or and index (1, 2, 3, ...), for example:

```
./c/inner/abc
./c/1/abc
```

Likewise, it can refer to a named input "in" as, for example:
```
./i/in
```

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
