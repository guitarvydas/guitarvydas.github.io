---
layout: post
title:  "Software Creativity"
---

If all I've got are berries and sticks, then all I can draw are cave-paintings before I run out of patience. 

If I've got oil paints, then maybe I can paint things in more detail before my patience runs out.

The tipping point for expressing creativity is to make it easy and rapid to do so.

If it takes several years to iterate Python, then I can only build certain kinds of programs.  

If I can whip up SCN's in an afternoon, then I might do things differently and build more interesting programs.

# Implementation

Current PLs are geared for Implementation.

Any PL that encourages a programmer to use `+` or to create user-defined data structures, encourages an Implementation mind-set.

# DI & Architecture

Any PL that encourages the use of only one paradigm, e.g. only Objects, only Functions, only Synchronous operation, etc., puts programming creativity in a box.

DI'ers should be free to choose any representation for a given problem and solution. 

DI'ers should be free to use multiple representations in one project. 

A DI'er should choose from a gamut of possible PLs.

## Dataless Languages

A _dataless_ language expresses only control flow and does not express _how_ to construct data structures that it uses.

A _dataless_ language can move data around using opaque handles to the data and, it can pass data to functions (and procedures), but it cannot "look inside" the data nor express how the data is constructed.

## Dataful Languages

A _dataful_ language expresses how to construct and name data, but does not provide control-flow operations.

Examples of data construction can be seen in just about every PL in the form of user-defined objects and classes.

For example, OOP languages encourage the definition classes of objects, and legal operations on such objects.

## Phases, Situations

Most PLs describe data in a way that makes all operations available at all times.

Compiler passes and UNIX pipelines describe operations that can only happen at given times.

For example, compilers might break down into several passes:
1. Scanning (lexing)
2. Parsing (checking syntax)
3. Semantic analysis (checking meaning)
4. Allocation (decisions about _where_ each datum is located (e.g. on the stack, in a heap, etc.))
5. Code emission (transpilation of the program into another format).

Programmers choose _arbitrary_ boundaries for time-related operations, e.g.
1. compile time
2. run time.

As shown above, (1) compile time, can be broken down into 5 components.

I believe that time-related phasing should not be restricted only to compiler-building.

## Gluing Languages Together

To be useful, a set of PLs for DI must be glued together to form a solution to a problem.

UNIX pipelines encouraged the use of multiple parts, programmed in different languages, to be glued together into a single solution.

Today's PLs expect one to create all parts using a single language and libraries.  FFI has become a method for breaking out of the single-language paradigm, albeit cumbersome. Docker is a partial solution to the multi-language problem. DLLs are yet another partial solution.

## Sychronous vs Asynchronous Design
Breaking free of synchronous design is an essential step for easily gluing languages together into seamless solutions.

## LEGO Blocks
DI needs to use software units that plug together like LEGO blocks.

Note that LEGO blocks all have the same API and that that API is simple - round posts that fit all other blocks.

Programmers have tried to use libraries as LEGO blocks, but, the API of libraries is too complicated and varied.

UNIX pipelines employed a simple API - lines of text. All interpretation of the data was performed by the components themselves.

It is possible to _stack_ types together, much like in a pipeline, to build up detailed type systems using only simple APIs.

A simple API might be the _message_ - an integer _tag_ and a chunk of _data_.

## Software Atoms

Software is composed of _atoms_.  Atoms can be composed into various other forms (_molecules_ to continue the analogy).

Assembler is a language / API of _atoms_.

Lisp is an HLL (High Level Language) that most closely consists of software atoms.

Lisp tends to have just about every kind of programming feature available.  Many other languages have started out as _molecules_ based on Lisp.

Lisp is often thought to be less human-readable than other PLs. Machine-readability is more important than human-readability for constructing phrases of atoms.

At present, I believe that _atoms_ consist of 3 aspects:
1. relation
2. subject
3. object.

Relational languages and XML most closely fit this model of _atoms_.

Note that, to extend atomic languages, one can provide syntax _skins_ and _layers_ instead of adding features to the atomic languages themselves. 

No _one_ syntax will fit _all_ problems. 

A notable example is the use of threading libraries with otherwise synchronous PLs.  Concurrency is fundamentally simple, except when expressed in synchronous form and when _all_ solutions use time-sharing and memory-sharing, even when not needed.

## PEG Parsing

PEG technology augments the ability create light-weight parsers.

Ohm-JS augments the ability to use PEG because it separates grammar from semantics (the rest of the code). Of course, it is _possible_ to write PEG pre-filters for other PEG technologies to accomplish the same effect as Ohm-JS, but this hasn't been done yet.


## Machine Readable Syntaxes

Programmers have concentrated on building "bigger and better" PLs with human-readable syntax.

To enable rapid turnaround for Software Creativity, automation - programs that write programs - can be used.

This requires an emphasis on _machine readability_ instead of human-readability.

## Diagrams as Syntax

Currently, PL syntax is limited to text, mostly in fixed fonts.

Creativity can be enhanced by enabling diagram-based syntax (DaS).

Note that diagrams-based syntax is not based on pixels and so-called _visual programming_.

Diagram-based syntax needs only a few primitives (already available in SVG as primitives):
1. rectangles
2. ellipses
3. lines
4. text.

DaS (Diagrams as Syntax) differs from text-based syntax in small ways, notably, the use of (x,y) coordinates instead of (line,offset) coordinates and the fact that cells can overlap (whereas character cells cannot overlap in most text-based PLs).

# See Also

[Transpilation of Racket PEG Code](https://guitarvydas.github.io)
[Blog](https://guitarvydas.github.io)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
