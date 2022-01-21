
---
layout: post
title:  "PREP Tool"
---

# Software Atoms WIP
Thinking out loud.  I reserve the right to change my mind.

I - currently - think that the SW Atoms are:
1. FP
2. long-running loop
3. CASE on Data Sequence 
4. CASE on Type 
5. Mutation
6. Object -- envelope of functions+state -- aka Actor
7. Exhaustive Search (Relational, PROLOG, miniKanren, etc, etc)
8. sequencing, synchrony
9. explicit-iness
10. concurrency

## Discussion
- [Sector Lisp](https://justine.lol/sectorlisp2/) is the epitome of FP 
- event-loops: aka Dispatcher, aka multi-tasking
- objects: aka Actors
- mutation: is supported by hardware, aka RAM, aka MOV instructions ; mutation is a fundamental aspect of CPUs - use of nesting (aka scopes) has, traditionally, been used to tame mutation (e.g. global variables) (assign-once is just an extreme version of scoping)
- isolation: is supported by hardware (MMUs) ; anti-dependency
- exhaustive search: aka Relational (PROLOG, miniKanren) (`!` (cut) and laziness are optimizations of exhaustive search)
- syntax: aka skin (syntax is frivolous, paradigms are important)
- npm, packages, Rust, etc, etc are epicycles swirling about the `isolation` atom
- The Stack is part of the FP paradigm ; The Stack is baked (hard-wired) into CPUs causing epicycles for all atoms except FP (observation: Relational programming is successfully backing away from The Stack) 
- CASE on Type is OO method dispatch, is this the same as (3) CASE on Data Sequence?
- CASE on Data Sequence is Parsing (often mis-optimized as Flags)