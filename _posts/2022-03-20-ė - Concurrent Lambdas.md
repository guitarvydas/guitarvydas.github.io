---
layout: post
title:  "ė - Concurrent Lambdas Working Paper (March 20, 2022)"
---
Looks like a function from the outside, but runs a dispatcher internally, allowing sensible diagrams to be drawn.

[lookup.asd](https://github.com/guitarvydas/dasl2/blob/dev/lisp/lookup.asd) (lisp project file)

[working diagram rough cut](https://github.com/guitarvydas/dasl2/blob/dev/eval.drawio) see lookup tab(s)


### Future

Once you have worked out the mechanisms for internal concurrency, it becomes "easy" to imagine other kinds of things, like internal state-tracking and Loop-ing...

- state machine lambdas (calls functions written as pure FP lambdas, receives a result, stores it, follow Harel-like StateChart hierarchy to enter/exit states)
- Loop lambda (calls function(s) written as pure FP lambdas, repeat)
	- one function as predicate - exit loop? continue looping?
	- one function as body of loop prior to predicate test
	- another function as body of loop after predicate test
	- `loop` { `call` body1(), `exit when` test(), `call` body2() }

One should be able to "compose" pure functions with concurrent lambdas with state-machine-lambdas with loop-lambdas.

## ė
As a working title for this concept, I'm going to use `ė`.

It is the Lithuanian letter "e" with a dot above it.

It is pronounced like Canadian "eh" or the English-language letter "A" (hard, not soft).

I almost chose another Greek letter, then realized that I could use any unicode character, then, almost chose a smily emoji, but, finally settled on `ė`.

[The choice is almost arbitrary, but, `ė` ties my two inherited cultures together.]

## Syntax Is Cheap

We need a toolbox that contains the Atoms of software.  Something like:
- pure functions (e.g. Sector Lisp, Lambda Calculus)
- state (history)
- looping.

Then, we can glue the Atoms together using any syntax we choose.

Syntax - language design - is equivalent to building up molecules using atoms.

PEG allows us to break out of the syntax prison. (Including the use of multiple languages (e.g. using balanced paren-matching))

Ohm-JS is even better than PEG.

FP taught us that variable names are inconsequential (in fact, this can also be understood by building compilers).

In my view, syntax is equally inconsequential.

## Pattern Matching

FP teaches that pattern-matching is King.  

Parsing is pattern-matching.

PEG is better-parsing.

Ohm-JS is better-PEG.

## Looping

We don't need TCO - tail-call-optimization.

We only need Looping.

TCO is make-work activity - an attempt to kludge looping into the functional paradigm.

We need a way to *compose* looping with pure functions.  

We do not need to add epicycles to the functional paradigm, nor to devise clever tricks that allow us to use the functional paradigm *everywhere*.

Sector Lisp is a wonderful example of a bloat-less functional paradigm.

Rhetorical Q: How do we *compose* Sector Lisp with Loop and State?

In my view, 
- Loop is a thing on its own.
- State is a thing on its own.
- Pure Functional is a thing on its own.

In my view, don't jam them all together, snap them together in new ways for every specific problem.

### Deprecating Loop and Recursion
Note that Looping doesn't even make sense in a distributed computing environment.  

A language for distributed computing does not have Loop (or Recursion) as a fundamental concept.  

A Component can always Send messages to itself if it wants to repeat a computation.

Looping and Recursion imply the use of a Stack.  This doesn't make sense in a distributed environment.  

A single CPU can have a single Shared Stack, but the idea of a Stack doesn't translate well into something that is sent on a thin wire.

The concepts of Loop and Recursion and Stack are so in-grained in our thinking that we feel it necessary to (cleverly) invent epicycles, like preemption, to accomodate long-running Loops.

These epicycles have caused us unanticipated grief in the past, e.g. priority inversion in the Mars Rover disaster (see my blog).

## On Diagrams
Diagrams - to normal humans - imply concurrency.

Boxes / ellipses / blobs on a diagram *look* like isolated entities.  And, that's how humans interpret diagrams.

Software is - currently - very synchronous.  As such, software programs defy diagramming. 

It is possible to draw diagrams of computer networks, because each computer on the network is isolated from the others (they synchronize only when they have to, otherwise, they run at their own speed (without implicit synchronization))).

It is possible to draw sensible diagrams of large chunks of software.

It is not possible to draw sensible diagrams of software at a fine grain, due to implicit synchronicity (for example, see my blog "CALL/RETURN Spaghetti").

There are 2 options:
1. Accept the fact that all programs, below a certain level, cannot be diagrammed.  You are stuck with lumps like Linux to shepherd isolated envelopes containing fancy calculators.
2. Find a way to optimize concurrency down to a lower level.  I propose Concurrent Lambdas (working name).  I think that every *function* should be concurrent (in fact, I'd be happier if every statement (line of code[^lines]) were concurrent, but, small steps first (`par` and thread libraries ain't it))).  In my view, Components send messages to one another - they cannot *call* each other directly.  For added flexibility, messages cannot be sent directly to peers, but must be sent upwards to the parent (Container) for routing.  Structured message-passing is hierarchical.

[^lines]: In fact, lines of code are *so* mid-1900s. I advocate switching to diagrams.  Diagrams can contain text (i.e. text is a subset of diagramming).  A unit of programming is The Component (concurrent), not the line-of-code (or function).  N.B. It is silly to draw diagrams of things that are perfectly fine as text, e.g. "a = b + c", but, there are other concepts that can only be meaningful as diagrams (e.g. networks of Components (where Components are not restricted to being 1-in-1-out things (M-in-N-out, where N >= 0 and M >= 0 [sic - 0]))).  A network can be represented as text, but, I don't find that meaningful (except as assembly code and core dumps).

## Drop-Dead Simplicity
The mechanism for interal concurrency is ridiculously simple.  Like the concurrency used in early computers
1. do something
2. `exit when` some condition is met
3. poll inputs
4. loop back to (1)

Preemption is a *tell* - a bad smell - that *something* is wrong / too-complicated.

In fact, *preemption* allows us to disobey the principle of locality-of-reference.  *Blocking* is done in two disparate places:
1. The Operating System
2. CALL / RETURN.

The O/S does preemption by pulling the rug out from under an app.  

The only reason that the O/S needs to do this is to allow for long-running Loops.

Preemption should be relegated to development systems.  

Well-behaved apps (i.e. products) should not interfere with one another and, hence, don't need preemption.

The only reason that product apps might mis-behave is that they are too complicated to understand (and tame).

### First-Class Functions and Closures

Operating systems implement closures in assembler and C.

The reason for this is bigotry.

Assembler and C programmers *thought* that Lisp (and dynamic languages) wasn't "as good" as C and assembler, so, they built part-of-lisp in raw assembler and C, the hard way.  Self-flagellation.

I suggest that we put concurrency directly into first-class functions and closures and get rid of Operating Systems.

## Concurrency Is Not Parallelism

Concurrency is a life-style.  

Parallelism is a greasy hamburger.

[Rob Pike Concurrency Is Not Parallelism](https://www.youtube.com/watch?v=oV9rvDllKEg)

It is possible to write programs that are concurrent but not parallel.

It is not possible to write programs that are parallel without, first, being concurrent.

Maybe concurrency is orthogonal to functions?  Like control-flow is orthogonal to data-flow.  (When you try to schmoo them together, you get a mess of complication).

Concurrency is a paradigm.  

Parallelism, though, is simply a problem-to-be-solved.  An optimization.

## See Also

[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)
[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC9EJr0nKHwadbHUtc5zHdmQ/videos)
[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Books](https://leanpub.com/u/paul-tarvydas.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 