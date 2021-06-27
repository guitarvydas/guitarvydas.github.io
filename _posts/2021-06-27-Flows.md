---
layout: post
title:  "Flows"
---

Computer software deals with two kinds of information:
1. data
2. control.

The term control-flow is used to describe the flow of control information.  Interestingly the term "data-flow" does not refer to the structuring of data information, but to a single kind of control-flow.

Currently, PLs[^pl] deal with mostly one kind of information - data - and tend to ignore the other kind of information - control.

Typical PLs, such as Python, conflate control information with data information. The language supports creation of _data structures_ as first-class entities, but tends to hide _control structures_ behind various forms of syntax, like _for_ loops and _if_ statements.

Some languages, like Scheme, provide Continuations that tend to combine data and control into a single datum.

Operating systems wrap control-flow into ad-hoc Continuations called _threads_[^stack].

Object-Oriented programming dealt with structured data design, but created unstructured control-flow design[^override].

The reaction to the problems caused by this perspective was to remove all semblance of control, culminating in FP[^fp] languages.

[^pl:] PL means Programming Language

[^fp:] FP means Functional Programming.

[^override:] Overrides and _super_ create control-flow dependencies that break the encapsulation of control information.  Inheritance is useful for data construction, but anathema to structured control-flow construction..  Getters and Setters are data-access operations, which can be separated from control-flow operations. _Blocks_ are closures.

[^stack:] Operating system threads conflate various issues that make Operating Systems appear to be high-art and magic. The (hidden) use of a global variable via the CALL and RETURN instructions is an example of such conflation.  The Stack is a global variable (an optimized list). Relational and FP languages attempt to escape the use of The Stack.

# Issues
## Separation of Concerns
Ideally, control-flow design should be separated from data design.

Data structuring is devoid of control information.

Control-flow structuring should, likewise, be dataless - devoid of data information[^ssl].

[^ssl:]  See S/SL (in References) for an example of a data-less language.

## Locality of Reference
Ideally, the description languages for data construction and for control-flow construction should provide locality-of-reference.

Simplifying, this means that all aspects of a design aspect should be visible to the reader in a single glance.

This used to mean that all information related to a portion of the design fit on a 24x80 display.  Today, it means that the information must fit in a _window_.

"Locality of Reference" also implies that there be no information leaks. 

Currently, such leaks are called "dependencies"[^locality].

[^locality:] If you can't see it all in one window, then it is not-local.  Libraries, as we know them, have this problem. _Import_ and _export_ syntax is often used to reduce the impact of such non-local references.

Dependency-managers hide such data leaks (and non-locality of reference).  

Dependency managers allow programmers to cope with information leaks, but build up a _dependency debt_ that usually needs to be addressed in the future. 

An insidious form of information leak is the use of _functions_!  Programmers write code that contains hard-wired calls to specific functions with hard-wired input parameters and hard-wired outcomes (return values and exceptions, all strongly typed).  DLLs[^dll] are an attempt to break out of such hard-wiring using indirection.  [IMO, the solution lies in the use of indirection and structuring of control flows (e.g. structuring component-based systems as trees).]

[^dll:] DLL means "Dynamic Link Library", often seen with file extensions such as `.DLL`, `.so` and `.dylib`.

Concatenative languages deal with hard-wired parameters and return values, but tend not deal with hard-wired function names and type names.

# Scoping (Nesting)

In computer science, it has often been the case that problems have been solved through the use of nesting - aka _scoping_.

## Structured Programming

Structured progamming was invented to alleviate the problems of _spaghetti_ control-flow arising from the use of _assembly language_ to program computers.

Basically, structured programming prescribed _nesting_ of control-flow as a solution to the problem of _spaghetti_ control-flow.

Today, most PLs provide _only_ structured programming constructs like `if-the-else`, `while`, etc. and eschew unrestrained control-flow constructs like `GOTO`.

Note that `GOTO` is needed in Denotational Semantics and has been rebranded as `CPS`.  CPS arises from the concept of first-class functions.  Functions are only loosely-structured, using packages and dependency managers. Types, likewise, are only loosely-structured in this way.

Further elaboration can be found at https://en.wikipedia.org/wiki/Structured_programming.

## Global Variables

The problem of _global variables_ was solved using _nesting_.

The terms _scoping_ and _local variables_ tend to be used instead of the term _nesting_.

The problem of _global variables_ was, in fact, a problem of locality-of-reference.  _Global variables_ were not considered to be a problem until programs grew to be "too large" (i.e. they didn't fit on one 24x80 screen or one window).

The "real" problem is one of _spaghetti dependencies_.  How to stop programs from becoming "too large"? 

## Object Oriented Programming

OOP prevented a solution for structuring data and divorcing data from implementation details.

In the process, OOP included control-flow in with data and conflated data-relative operations, such as _getters_ and _setters_ with non-data-relative operations.

_Inheritance_ is a useful way to organize data.

_Inheritance_ is a poor way to organize code.  In fact, I argue that one should use the opposite of inheritance - I call it _composition_ - to organize code.  _Composition_ is seen in StateCharts - the parent statemachine can override operations of children statemachines, which is exactly the opposite of inheritance (where children methods can override parent methods).

Note that this is _not_ a binary programming choice - one or the other (inheritance vs. composition).  Conflating the two possibilities leads to accidental complexity.  PLs should allow for orthogonal desription of data structures vs. control-flows.

## Syntax

Syntax is, currently, the manner for dealing with control-flow descriptions. 

I believe that control-flow description is orthogonal to data description.

From this perspective, one should use two languages for any program - 

1. a data description language
2. a control-flow description language

and, that neither language should contain syntax for the other kind of description.  One could use a third language to plumb programs together, for example, like `/bin/bash`. (I contend that syntax is cheap, languages for plumbing programs together can be designed to be "better", and more austere, than `bash`)

## Pattern Matching
The trend in FP is to use _pattern matching_ to separate control information from data information.

Separation of concerns is achieved by relegating all control-flow to an engine that is not part of the description language.

Pattern matching is well-understood, albeit under a different name - "parsing".

## Denotational Semantics

Denotational Semantics is the field of describing programming languages using functional notation.

Control-flow, in Denotational Semantics, is most often handled through the use of `GOTOs` (rebranded as CPS, first-class-functions, continuations, etc.).

## Data Flow

As mentioned earlier, "data flow" refers to a style of control-flow, not to data structuring.

In the data-flow style, the operation of a component is suspended until all of its inputs have arrived.  The classic example is a `+` operator, `result = b + c`.  `Result` is computed only when, both inputs, `b` and `c` are available.

In contrast, FP requires that _all_ inputs arrive at a component (a _function_) at the same time.  The component is never suspended and it operates immediately and returns its results all at the same time.  Complications caused by this perspective are being resolved through the use of features like _futures_. Note that FP assumes that there is a single _happy path_, i.e. the function succeeds in returning a value(s) and everything else is considered to be an _exception_.  Programmers are discovering the limitations of this model as they delve into distributed programming, e.g. internet, blockchain, p2p, etc.

## Control Flow

The current model for control-flow - syntax - is based on assumptions related to 1950's computer hardware - e.g. a single CPU[^cpu] and expensive memory.

These assumptions are being broken as programming evolves towards distributed architectures and internet solutions.

[^cpu:] Hence, the name _central_ processing unit.

## Deep Recursion, Long-Running Loops

The 1950's model of computing has resulted in the notion that programs can contain deep recursion and long-running loops.

Neither of these constructs is appropriate for distributed programming.  Programmers _can_ create distributed programs, but ths is harder due to accidental complexities introduced by the underlying assumptions.

Notably, the assumptions have led programmers to using full-preemption and operating systems.  

Full preemption has caused many accidental complexities, e.g. the Mars Pathfinder disaster https://www.rapitasystems.com/blog/what-really-happened-software-mars-pathfinder-spacecraft[^1]. 

[^1:] This problem was later repaired with the band-aid called "priority inheritance".

## State

Programmers conflate the various uses of _state_ and lump them together.

I discuss this further in https://guitarvydas.github.io/2021/03/30/State,-Analysis-of.html. 

## StateCharts

State machines suffered, early on, from a problem called _state explosion_.

An small example of _state explosion_ is demonstrated in _Fig. 20_ of the paper below.

StateCharts - developed by David Harel - solve the _state explosion_ problem using nesting.

I discuss StateCharts further in https://guitarvydas.github.io/2020/12/09/StateCharts.html and https://guitarvydas.github.io/2021/02/25/statecharts-(again).html.

Note that many "successes" in programming have been built on top of the _state_ paradigm, e.g. operating systems, YACC, LEX, REGEXP, etc.

## Threads

_State_ has been conflated with several issues, including control-flow, the global stack, etc.

_Threads_ are one way to lasoo these issues and hide them.  

Notably, _threads_ isolate the stack used by one program from other programs (using hardware assist, wrapped by libraries called _operating systems_).

As programmers approach distributed architectures, the limitations of _threads_ become more apparent.

_Threads_ are more like assembly-level operations provided on a single CPU than a high-level concept useful for programming distributed systems.

## Dataless

See the References section for S/SL - a dataless language that was, ostensibly, used for constructing compilers (aka "big" programs).

## GOTOs, CPS

As mentioned earlier, CPS is a re-branding of the concept of GOTOs.  In fact, CPS is more "powerful" than GOTOs.

The problem with GOTOs was not the GOTOs themselves, but the unstructured use of GOTOs.

PL designers conflated two issues - data construction and control-flow construction - which resulted in accidental complexities.  

Creating languages that address both problems at once creates difficulties and unnecessary complexity.

## Scalability

Components are scalable only if they are not inter-related.

Scalable components cannot have dependencies on one another.

https://guitarvydas.github.io/2021/06/17/Dags.html

## Type Checking

Currently, most PLs provide a handful of hard-wired types and a way for programmers to define further types. 

## Input Validation

Programmers are accustomed to writing specialized code to further validate data.

This is but another form of type checking.

The fact that three forms of type checking exist (hard-wired, programmer-defined, input validation) is a _tell_ that the concepts of type checking are overkill and non-uniform.

## Absolute Naming

Currently, most PLs create names that are _absolute_ and global to the whole application.

Modules, packages, etc. have been invented to constrain the use of such names.

# Solutions

## Dependencies

At present, I believe that dependencies are a first-order problem.

Hidden dependencies exacerbate the problem.

Languages must be designed to allow construction of independent units. (For example, calling functions by-name should be disallowed).

Package managers and build managers (like _make_) facilitate our use of dependencies, instead of making such dependencies more obvious.

Libraries that depend on other libraries (ad infinitum) contain _hidden_ dependencies build up _dependency debt_.

### Visualizing Dependencies

I believe that diagrams show dependencies more readily than textual code.

Whiteboards are found in every software shop.  

This observation is a _tell_ - it indicates that _something_ about current PLs is inadequate.  

(My suggestions follow).

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

Components that provide _all_ outputs in single block are the exception, not the rule.

### Exceptions

Exceptions are not exceptional.

Exceptions produced by components are the same as all other outcomes produced by components.

The problems and the solutions dictate which outcomes are considered to be erroneous.  _Software Architects_ design solutions that produce the desired outcomes.

## Ports

Software components have input _and_ output ports.

Most current PLs have APIs that imply synchronous operation.

### One Universal Type

Components are plugged together port-to-port where ports have a universal, simple type, e.g. _message_.

The above does not imply that type-checking is discarded.

Types checking is done in a pipeline, from simple to more complex.  

Type checkers are, already, interpreters that filter incoming information and raise errors.

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

Most programmers quote Windows 3.11 as a failed attempt at mutual multitasking, but do not balk at the idea that applications may contain bugs (esp. early on).

Preemptive multitasking is a special technique - an exception, not the rule - that needs to be employed when building operating systems.  There are very few programs that need to use this technique, e.g. the software called _Linux_, _Windows_, _MacOS_, etc.

Applications do not need preemptive multitasking internally.  There is no need to pay the cost of preemption[^2] when it is not needed.

[^2:] Preemption does have costs, e.g. (1) hardware facilities, (2) accidental complexities, (3) overkill use of l libraries (often called "operating systems"), etc.

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

A Dispatcher routine invoked _ready_ components in a random order.

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
