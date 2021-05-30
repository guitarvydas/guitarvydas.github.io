---
layout: post
title:  "How All This Stuff Ties Together (WIP)"
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
- programming becomes the art of solving problems instead of fitting problems to fit specific languages
- one sees that there are many "silver bullets", not just one (the Silver Bullet used depends on the Problem and on the Architect)
- Software Engineering - like Construction Engineering - becomes fully realizable.

One of the problems of software design is that we (the royal we) have been thinking about software _only_ in a synchronous manner (even when we try to solve asynchronous problems).

I claim that we need to think about _asynchronous software components_ and _relative naming_.

Currently we talk about types and functions as if they are not hierarchical and are absolute.  Functions can refer directly to other functions, and so on.

This mindset has caused many accidental complexities, like the notion of using Operating Systems and the windmill of one-languge-to-rule-them-all.

I claim that we should be thinking of _notations_ instead of _languages_ and that we should learn about _paradigms_ instead of specific _languages_[^smalltalk].

I claim that we should learn about the limitations of each paradigm and that we should learn when to apply certain paradigms to certain sub-problems[^relational].

[^smalltalk]: For example, learning OOP is good, learning the syntax of Smalltalk is less good.  Language notations that support OO principles blink into and out of existence, while the fundamental principles espoused by OO (e.g. encapsulation) carry on being relevant.

[^relational]: For example, _relational programming_ is a good paradigm for searching, while it is not a very good paradigm for producing output (on a screen or on paper, etc.).  For example, OO is a good paradigm for encapsulating data, but less good for encapsulating control flow.  For example, FP is a good paradigm for creating calculators, but less good for creating asynchronous systems. It all depends on the problem-at-hand (and on the Architect(s) wielding the tools).

This leads to a notation that treats software components in a relative manner. We've seen this in UNIX, but have not seen it in popular programming languages, e.g. all variables are "flat" names and are allowed to break through the boundaries of components and to refer to objects in other components. 

# Spaghetti Architecture
When this (absolute naming) was recognized in relation to Control Flow, it was called Spaghetti Programming.

I call this same phenomenon in today's software, _Spaghetti Architecture_.

# ASC Notes
## 
# 

# ASC Examples
## ASC Notation
## ASC Notation to Common Lisp
## ASC Notation to JavaScript
## ASC Notation to Python
## ASC Notation to WASM
## 
# 

# Instructional
## PROLOG For Programmers
	[PROLOG For Programmers](https://www.youtube.com/watch?v=QOYAHoLiyg0&t=205s)
## PEG - Implementing a Simple Transpiler
## 
# 

# Miscellaneous
## Languages are Cheap
## Code is Cheap, Design is Hard
## PL Really Means Notation
## Paradigms
### Concurrency
## Discard Operating Systems
## Two Syntaxes for Every PL
## 
# 

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
