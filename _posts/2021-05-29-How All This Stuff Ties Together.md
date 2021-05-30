---
layout: post
title:  "How All This Stuff Ties Together"
---
# Introduction

I have written some 180 essays on various topics. (See below).

These may seem to be isolated islands of writing, but, in my mind they all tie together towards one goal.

The goal is _Asynchronous Software Components_.

Concurrent computing and compiler-building and EE (Electrical Engineering) and Physics[^ownership] are all tied together, at least in my mind.

[^ownership]: For example, Rust's notion of _ownership_ relates to the idea of data as Physical objects. (FTR, ownership appeared in FBP in the 1960's and in my own consulting work.  I discarded ownership in lieue of garbage collection).

When one adopts the principles of _ascs_, 
- computing looks different (we can think in terms of isolated components instead of calculators)
- many problems become much easier to solve
- programming becomes the art of solving problems instead of twisting problems to fit specific languages
- one sees that there are many "silver bullets", not just one (the Silver Bullet used depends on the Problem and on the Architect)
- Software Engineering - like Construction Engineering - becomes realizable.

One of the problems of software design is that we (the royal we) have been thinking about software _only_ in a synchronous manner (even when we try to solve asynchronous problems).

I claim that we need to think about _asynchronous software components_ and _relative naming_.

Currently we talk about types and functions as if they are not hierarchical and are absolute.  Functions can refer directly to other functions, and so on.

This mindset has caused many accidental complexities, like the notion of using Operating Systems and the windmill concept of one-languge-to-rule-them-all.

I claim that we should be thinking of _notations_ instead of _languages_ and that we should learn about _paradigms_ instead of specific _languages_[^smalltalk].

I claim that we should learn about the limitations of each paradigm and that we should learn _when_ to apply certain paradigms to certain sub-problems[^relational].

[^smalltalk]: For example, learning OOP is good, learning the syntax of Smalltalk is less good.  Language notations that support OO principles blink into and out of existence, while the fundamental principles espoused by OO (e.g. encapsulation) carry on being relevant.

[^relational]: For example, _relational programming_ is a good paradigm for searching, while it is not a very good paradigm for producing output (on a screen or on paper, etc.).  For example, OO is a good paradigm for encapsulating data, but less good for encapsulating control flow.  For example, FP is a good paradigm for creating calculators, but less good for creating asynchronous systems. It all depends on the problem-at-hand (and on the Architect(s) wielding the tools).

This leads to a notation that treats software components in a relative manner. We've seen this in UNIX, but have not seen it in popular programming languages, e.g. all variables hav "flat" names and are allowed to break through the boundaries of components and to refer to objects in other components. 

# Spaghetti Architecture
When absolute naming was recognized in relation to Control Flow, it was called Spaghetti Programming.

I call this same phenomenon in today's software, _Spaghetti Architecture_.

# ASC Notes
A syntax for relative, asynchronous, software components.
[ASC Design Notes](https://guitarvydas.github.io/2021/05/29/Asynchronous-Software-Components-Design-Note.html)

# Instructional
## PROLOG For Programmers
	[PROLOG For Programmers](https://www.youtube.com/watch?v=QOYAHoLiyg0&t=205s)
## PEG - Implementing a Simple Transpiler
[Transpilation 101](https://guitarvydas.github.io/2021/05/29/Transpilation-101.html)
## Youtube
- The Holy Grail (2:32)
- Visual Programming (2:30)
- Control Flow (5:51)
- Prolog For Programmers (15:44)
- Divide and Conquer (35:18)
[Computing Simplicity](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy50fIg)
## 
# 

# Miscellaneous
## Languages are Cheap
## Code is Cheap, Design is Hard
## PL Really Means Notation
Programming languages are notations.

Programming languages are notations for something deeper - paradigms.

Programming languages are notations that take a looong time to build.

Notations can be built in less than a day using modern tools (e.g. Ohm-JS (PEG) and Toolbox Languages).
## Paradigms
### Concurrency
### OOP
### FP (Functional Programming)
Good paradigm for build fancy calculators. 

Less good for building distributed systems.

A calculator is a one-in-one-out thing. 

Real life tells us that we deal with one-in-many-out things, though.

For example, time-outs should be first-class things, not relegated to the back burner.

Exceptions are edge-case syntax added as a bag onto the side of one-in-one-out syntax.

Q: What about parameters that don't want to come in one blob?

Q: What about return values that don't want to be sent in one blob?

Real life says that objects are autonomous and can send information _at any time_.

Autonomous --> asynchronous.

Analogy: synchronous == human consciousness. Asynchronous == all the rest (the human body's autonomous system).  The book "The Inner Game of Tennis"[^1] does not imply that consciousness is better than sub-consciousness and uses the terms "self 1" and "self 2" instead.

[^1]: The best book about golf (Shawn Clement). 

Async should be the default, sync should be an exception. E.G. we can use sync techniques _when allowed to by the problem_.

Force-fitting async into sync notations has brought us epic failures, like threads and multitasking (which crashed the Mars Rover, for example).  

It is hard to reason about async problems with one hand tied behind your back, e.g. by forcing oneself to use sync notation _only_ (a form of self-flagellation).

CPS is another word for GOTO.
## Discard Operating Systems
## Two Syntaxes for Every PL
## 
# 

# See Also

[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html)

[The Inner Game of Tennis](https://www.goodreads.com/book/show/905.The_Inner_Game_of_Tennis)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
