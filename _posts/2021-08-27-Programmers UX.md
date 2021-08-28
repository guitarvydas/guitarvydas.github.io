---
layout: post
title:  "Programmers' UX"
---

Programming languages and IDEs are stuck in the 1950's.

In contrast, UXs for non-programmers have advanced into the 2020's.

Non-programmers use _windows_ embodied in operating systems like Windows, MacOS and Linux.

Programmers still use languages which are text-oriented, use simple bitmaps (aka _characters_) with cells arranged in a non-overlapping manner indexed by line and column numbers.

# Diagrammatic Programming is _Not_ Visual Programming
Visual programming has come to mean pixels.

Diagrammatic programming (DaS - Diagrams as Syntax) is based on a very few simple shapes, namely
- rectangles
- ellipses
- lines
- text.

Diagrammatic shapes can overlap and are indexed by (x,y) coordinates.

# SVG

SVG can represent the simple shapes required by diagrammatic programming. 

SVG is a superset of what is needed for DaS.

# Diagrammatic Programming Editors and IDEs

Currently, only [diagrams.net[(https://www.diagrams.net) (aka drawio) seems to under-utilize SVG and provide simple editing of compilable diagrams.

Diagrams.net, in fact, uses a data format - mxGraph - which is a per-cursor to SVG.

It is possible to parse mxGraph files.  This is shown in [langjam entry](https://github.com/guitarvydas/jam0001/tree/main/guitarvydas_ (see https://github.com/guitarvydas/jam0001/blob/main/guitarvydas/README.md)

# What is the Use-Case for Diagrammatic Programming?

DaS - Diagrammatic Programming - is useful _only_ if it can express programs which are not handled by existing textual languages[^1].

[^1]: For example, `a = b + c` should never be expressed in diagrammatic form, since the textual form is already available and is convenient.

Existing textual languages are geared towards Implementation - implementation of code, implementation of data structures, syntax checking and type checking.

DaS can be used to express _software architecture_.

Diagrams lead to nested diagrams, which leads to _structured_ software architecture (DI - Design Intent).

Diagrams show leakage and dependencies between software components.

In contrast, textual languages tend to elide details such as synchrony and CALL/RETURN (a form of synchrony).

Diagrams can make such details explicit - e.g. sequencing can be shown as arrows from one block to another and parallelism can be shown as arrows that branch from one component to more than one other component.

## Synchronous Components

<img src="https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-08-28-Simple%20Diagrams-Synchronous.png?raw=true" alt="2021-08-28-Simple Diagrams-Synchronous.png" style="zoom:67%;" />

## Asynchronous Components

<img src="https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-08-28-Simple%20Diagrams-Asynchronous.png?raw=true" alt="2021-08-28-Simple Diagrams-Asynchronous.png" style="zoom:67%;" />

## Nested Components

<img src="https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-08-28-Simple%20Diagrams-Nesting.png?raw=true" alt="2021-08-28-Simple Diagrams-Nesting.png" style="zoom:67%;" />

## Ports

<img src="https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-08-28-Simple%20Diagrams-Ports.png?raw=true" alt="2021-08-28-Simple Diagrams-Ports.png" style="zoom:67%;" />

# Locality Of Reference

Often, a major success factor in general programming language design, comes from localizing objects.

An example of locality of reference is the use of scope variables in place of global variables.

An example of locality of reference is the use of structured programming in place of ad-hoc GOTO programming (if, while, etc., constructs that constrained the use of GOTOs.).

Diagrammatic programming can have the same effect, but at the level of _software achitecture_.

## Nesting

Nesting can show how software modules are constructed

Nesting can show flows that break through the boundaries of components.  This is also known as _dependency_.

## Ports

Ports contstrain the flow of data between software components.

Data flow constraints improve the locality of reference for information.

# See Also

[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy5)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
