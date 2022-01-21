# Paradigms
Paradigms are fundamental models of - in this case - software design.

Syntax is a skin draped over each paradigm to make the paradigm more accessible.

More than one syntax can be draped over a single paradigm, e.g. multiple OO languages are different syntaxes for essentially the same concepts[^1].

[^1]: The different OO languages vary in degrees along different dimensions, e.g. purity vs. optimization, etc.

Paradigms are more important than syntax.

Below is an incomplete list of paradigms.

[Other articles describe how to invent syntaxes and how to drape them over paradigms]

## Functional
- All code and constants and data are written as functions.
- The benefits of FP are often conflated with isolation and explicit-iness (see below)
- FP syntax (*everything-is-a-function*) is a normalized syntax.  
- When combined with immutability, FP notation can be manipulated manually or automatically to reduce and optimize code sequences.

Normalized syntax is good for machine-readabilty.

Optimizations can map functions into more-efficient code and representations.

FP notation is useful for describing calculators, but less useful for describing sequencing and history (statefullness).

Originally, it was thought that computers were good only for calculating ballistics, hence, it was thought that FP was The Answer to programming computers.

Computers are, also, useful for sequencing - machine control, DAWs (Digital Audio Workstations).

Computer are, also, useful for reacting to event-driven inputs, e.g. GUIs, sensors, etc.

Computers are, also, useful for creating long-running loops.

Computers are, also, useful for creating *event loops* like those found in windowing systems.

Although it can be used, FP is not the most appropriate paradigm for describing sequencing and event-driven inputs and long-running loops and asynchronous processes.

Constants are considered to be anonymous functions, for example
```
(lambda () 1)
```
Might be used to represent the small integer constant 1.  Later optimizations can map this representation into more efficient CPU-specific operations / operands.

## OO
- an object is an envelope that contains functions and data (aka *state*)
- *everything-is-an-object-with-state* including constants
- suffers from being unwittingly implemented in a synchronous paradigm using synchronous languages
- add multi-tasking => Actors
- suffers from being implemented using FP CPUs in synch paradigm
- optimizations can map various objects to more efficient representations, for example small integers can be mapped to CPU operands instead of being implemented as full-blown objects

The small integer constant 1, might be represented as an object
```
prototype BasicInteger {
function + ( ... )
function - ( ... )
function * ( ... )
function / ( ... )
...
object 1 is like BasicInteger {
  self.value = 1
}
```


## Exhaustive Search
- Query that returns all possible answers
- fundamental mechanism of PROLOG
	- but, PROLOG added optimizations, since it used backtracking, which was expensive in 1950's technology
	- see [Nils Holm's PROLOG Control in 6 Slides](https://www.t3x.org/bits/prolog6.html)
- miniKanren accomplishes exhaustive search without using backtracking
## Synchrony
- a programming paradigm that is useful for building calculators
- it was originally thought that computers were just calculators (for calculating ballistics)
- computers also can perform sequencing, which does not fit easily into the synchronous paradigm
- rendezvous
## Asynchrony
-  thread libraries are band-aids ; glue-on asynchrony
- enables isolation (> encapsultion) => black boxes
- fundamental mechanism for distributed
- cannot use stack (lest you send the stack down a single wire)
- often confused with parallelism (parallelism is an optimization, concurrency is a paradigm)
## Diagrams
- break free of text-only representations
	- reduce accidental complexity of forcing solutions into text-only cubby-holes
- "diagrams" fills the gap between text-only and full-blown VPL (Visual Programming Languages)
- supported by SVG (rectangles, ellipses, lines, text)
- "diagrams" => hybrid of simple graphical elements *plus* text

## Recursion
not Loops
## State
### Case on Type
- OOP
### Case on History
- StateCharts (structured state machines)
### Case on Sequence of Datums
- parsing (Ohm-JS <== PEG)
## Nesting
- aka "scoping"
- aka "namespaces"
- aka "packaging"

## Parsing
- aka "pattern matching"
- pattern matching currently in vogue in FP languages

## Dependency
- seen to be a bad idea
- =>violates isolation
## Isolation
- build and forget
- no dependencies between components (data dependencies *and* control-flow dependencies)
### Encapsulation
- "encapsulation" is an isolation wannabe, but fails to encapsulate control-flow
## Control Flow
- 1/2 of Turing Machine
- like the playback head in a tape recorder
- distributed computing
	- internet
	- p2p
	- IoT
	- autonomous robotics
## Data Flow
- 1/2 of Turing Machine
- like the magnetic tape in a tape recorder

## Explicit-iness
- unambiguous
- *very clear and complete ; leaving no doubt about the meaning* (from [Merriam-Webster Dictionary](https://www.merriam-webster.com/dictionary/explicit))
- anti-hidden
- example: in Denotational Semantics, the *environment* is passed as an argument to all functions
- counter-example: in modern CPUs with a stack pointer (SP), the stack is hidden and made non-explicit (this favours running FP on CPUs while de-emphasizing other possible paradigms (multi-tasking can only be simulated on modern CPUs))

## Concurrency
## Synch
- rendezvous
- ACK/NAK
- gears

## Manipulating Code
### Macros
### Functional Programming
### Compilers
### Example
edit.bash for slread grammar -> slread glue

## The Fundamental Atoms Of Software
1. Functional Programming
2. long-running loop ; aka "event loop", aka "main loop"
3. CASE on Type (is this (4) where data sequence is expression of Type?)
4. CASE on data sequence 
5. Mutation
6. Object -- envelope of functions+state -- aka Actor
7. Exhaustive Search (Relational, PROLOG, miniKanren, etc, etc)
8. sequencing, synchrony
9. explicit-iness
10. concurrency
11. Isolation

### FP - Functional Programming
(1) FP is emobodied in [Sector Lisp](https://justine.lol/sectorlisp2/)