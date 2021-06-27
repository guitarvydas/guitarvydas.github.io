---
layout: post
title:  "Software Components (Abridged from Flows)"
---

# 

## Dependencies

At present, I believe that dependencies are the first-order problem.

_Hidden_ dependencies exacerbate the problem.

Languages must be designed to allow construction of independent units. (For example, calling functions by-name should be disallowed).

Package managers and build managers (like _make_) facilitate our use of dependencies, instead of making such dependencies more obvious (and painful to use).

Libraries that depend on other libraries (ad infinitum) contain _hidden_ dependencies and build up _dependency debt_.

### Visualizing Dependencies

I believe that diagrams show dependencies more readily than textual code.

Whiteboards are found in every software shop.  

This observation is a _tell_ - it indicates that _something_ about current PLs is inadequate.  

(My suggestions follow).

## Little Things

The Little Things matter.

If you think of parsers as needing tokenizers (scanners), it changes the way you approach a solution.

How does your approach change if you though that parsers were as easy-to-use as REGEXPs?

https://guitarvydas.github.io/2021/04/26/What-If-Making-A-Compiler-Was-Easy.html

## Asynchronous Components

Software components are _asynchronous_ by default.

Synchronous components are the exception, not the rule.

### Lifetimes

Software components "live forever" (like web servers).

Components that wake up and die are the exception, not the rule.

### Parameters

Software components can be supplied inputs at different points in their lifetimes.

Components that need _all_ inputs at once are the exception, not the rule.

Componenets that need _all_ inputs delivered in single blocks are the exception, not the rule.

### Outcomes

Software components can produce outputs at various points in their lifetimes.

Components that provide _all_ outputs at the same time are the exception, not the rule.

Components that provide _all_ outputs in single blocks are the exception, not the rule.

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

The above does not imply that type-checking is discarded.

Types checking is done in a pipeline, from simple to more complex.  

Type checkers are, currently, interpreters that filter incoming information and raise errors.

Type checkers become regular software components, with one input and two outcomes (data to be checked, data that satisfies the check, error condition, respectively).

Multiple checks can be inserted into the pipeline, suiting the problem-at-hand.

Not _all_ software components need to fit this simple - one-in-two-out - model.

## Layering

Components are built in layers.

No layer contains more units than can be comprehended, e.g. 7±2.

Components can, themselves, contain layers, recursively.

##  Loops

Long running loops and deep recursion are not allowed.

Long running loops and deep recursion can be broken into smaller steps by sending _continue_ messages to the looping component(s) (or self-sending such messages).

Compilers can insert _yields_ into loops (say, the bottom of a loop) and new syntax can be used to flag deep recursion for automated breaking-up.

This is, essentially, mutual multitasking.

Most programmers quote Windows 3.11 as a failed attempt at mutual multitasking, but do not balk at the idea that applications may contain bugs (esp. early in the development of the application).

Preemptive multitasking is a special technique - an exception, not the rule - that needs to be employed when building operating systems.  There are very few programs that need to use this technique, e.g. the software called _Linux_, _Windows_, _MacOS_, etc.

Applications do not need preemptive multitasking internally.  There is no need to pay the cost of preemption[^2] when it is not needed.

[^2:] Preemption does have costs, e.g. (1) hardware facilities, (2) accidental complexities, (3) overkill use of libraries (often called "operating systems"), etc.

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
