---
layout: post
title:  "PEG vs. Lisp Macros"
---

Q: What are the differences between PEG and Lisp Macros?

This is actually a multi-tier question.

Knowing the details about the differences does not inform you about _why_ the differences matter.

Let's start small.

# Lisp Macros
- a Lisp program is a _list_ of things (atoms and other lists)
- Lisp comes with a bunch of features for manipulating lists
- hence, Lisp features can manipulate lisp programs (which are just lists)
- a Lisp compiler compiles a list - a Lisp program
- Lisp macros are compile-time break-outs that allow you to manipulate lists - programs - before the compiler gets to see them
- Lisp macros are nicely integrated into the Lisp compiler and you don't need to do anything special to invoke a macro
- in Lisp, everything looks like a list
- in Lisp, a function looks like a list (the compiler assumes that the first thing in the list is a function)
- in Lisp, a macro looks like a list
- lisp macros look like lisp functions (you declare a function using the DEFUN keyword but you declare a macro using the DEFMACRO keyword
- Lisp afficianodos were not completely satisfied with Lisp's list manipulation features and added a bunch of hieroglyphics to perform common operations, like list splicing, etc. (the hieroglyhpics are symbols like the back-tick, comma-at and comma e.g.
```
`
,@
,
```
resp...

# The Detailed Differences Between PEG and Lisp Macros:
- Lisp macros work only on lists of things (atoms and lists), whereas PEG works on _characters_
- PEG uses REGEX-like syntax, e.g. `*/+/?` whereas Lisp macros use things that look like function names
- Lisp provides low-level operators, like `+` and `-` on numbers, whereas PEG does not understand numbers (and other data structures).

# Allowing is not the Same as Encouraging
In Lisp, you can do `everything` that PEG can do, and more.

Psychologically, this is _not_ a good thing.

In PEG, you can only do one thing - parse text.

In Lisp, you can do many more things.

# Details Kill
[Details kill](https://guitarvydas.github.io/2021/03/17/Details-Kill.html).

Too many degrees of freedom doesn't give you freedom, it gives you confusion.

# Specialization
- PEG is specialized for parsing, _only_. (In other words, PEG is DSL for parsing).
- Lisp isn't specialized for anything in particular, it is a _general purpose_ language.  You can do parsing in Lisp, and, you can do a bunch of other stuff.

# Implementation
Lisp is specialized for implementation of all sorts of programs.

PEG is specialized for specification of parsers.  Ohm-JS takes PEG-like specifications and converts them into parsing apps (using JS as the toolbox language).

[Aside, Parser Combinators are kinda the same. Combinators are specialized for parsing, but allow access to lower-level features of the language. If you replace "Lisp" with, say, "Haskell" in this note, you get the same answer.]

# DI - Design Intent and Architecture
The best way to understand an architecture is to see it expressed directly.

A poor way to understand architecture is to reverse-engineer it from a pile of details.  Lisp, Haskell, Python, etc. all suffer from this problem. These are languages for specifying Implementation, not for specifying Architecture.  You have to reverse-engineer Architecture from the code.

# Why?
Everything is a fractal.  This means that everything can be subdivided.

Are you wanting to deal with DI (Design Intent, aka Architecture)?

Are you wanting to deal with Implementation?

The worst thing to do is to try to shoe-horn everything - DI and Implementation - into one language.

# PEG
PEG enables us to write notations[^1] easily.

[^1]: Remembering that I use the word _notation_ to mean a light-weight DSL.

There is no longer any excuse for using only one language for _everything_.

# Lisp Macros
I have learned a lot from Lisp.

I conclude, though, that a lot of the features of Lisp should be broken out of Lisp and made into stand-alone features, e.g.
- an expression language for Implementation[^2]
- a Macro Language for parsing
- a rapid-prototyping language for debugging concepts
- a toolbox language for building better syntaxes and notations
- etc.

Lisp started out as a simple language for rapid prototyping. Then, it became a kitchen sink for every kind of reseach-y idea. The ideas that stuck to the wall were unioned together and Common Lisp was the result. The CL standardizers had an agenda - they wanted a language that produced code that was as efficient as the FORTRANs of the day. As a result of this agenda, Lisp lost a lot of its debugability flavor (it _looks_ like it's still there (break, condition handlers, etc. but its all mixed in with complex features that reduce debugability (current SBCL is the epitome of anti-debugability (e.g. SBCL gives multi-line warnings that don't help you find the real problems)))))

[^2]:Note that Engineering is not Implementation.  We need a language for Architecture _and_ we need a language for Engineering. We already have multiple languages for Implementation (e.g. Python, Javascript, Haskell, etc.).  Engineering is the stuff that fits between Architecture and Implementation. Engineering makes Architectural ideas do-able. Implementation is code. Currently, we do everything in one language and pay to have all software custom-built, where we could chop it up into Architecture/Engineering/Implementation/Testing, etc, etc. and pay only for what we need.

# Conclusion - PEG vs Lisp Macros
If you have to use only one language (something that I advise against), Lisp is "good" in that it doesn't restrict which paradigms you can use. Furthermore, it is possible to elide details by using Lisp macros. 

Lisp is OK, but a bunch of nicely fitting sub-languages would be better.

Back to the original question - how is PEG related to Lisp macros?  If you've built big applications using Lisp macros, then you've tasted the concept of _separaction of concerns_. Probably, you've separated DI from implementation and elided the differences using macros.  

This is workable, but not my ideal. 

Lisp macros teach you about parsing and separation of concerns.

PEG should be familiar to anyone who uses Lisp Macros.

PEG might be a bit weird if you've only used 3GLs and have never built a DSL-ish micro language.

The psychological differences between PEG and Lisp actually matter more than it would seem. Lisp lets you build parsers, so why would you need PEG? Lisp macros get even closer.

When you get good at this stuff, the little differences begin to matter more.  I think that I know how to build Architectures vs. Implementations, yet, I can't help but try to do Implementation-y things in my Architecture code when I use a single Implementation language for everything.

I need to use a notation that reminds me to separate concepts.

For example, you _can_ write OOP code in assembly language, but you tend not to.  OOP languages stop you from doing anti-OOP things in your code[^3]. Likewise, we need languages that stop us from doing anti-DI things in our code.  I _can_ write compilers in Lisp or C or Python, but when I use S/SL it reminds me to separate the compiler DI stuff from the implementation stuff, which, in the end, makes it easier to write the compilers.  People are "discovering" this kind of thinking when they use super-strongly-typed languages like Haskell.  "It just works" is not because of Haskell, it's because they've thought the design through, led by the boundaries imposed by Haskell's strong type-checking.  Strong typing is but only _one_ way to think about an Architecture, but most people blame success on strong typing. 

[^3]: For the record, 1st-class functions were supported in C, but not encouraged.  Closures were built into Lisp 1.5 in 1956, then ignored and re-built in assembler and C to make UNIX threads.  Garbage collection - malloc () - appeared in K&R.  Changing the notation helped us use these concepts pervasively.  The difference is "just" a psychological detail.
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
