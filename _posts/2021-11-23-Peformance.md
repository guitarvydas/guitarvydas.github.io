---
layout: post
title:  "Performance"
---

# Synopsis
This note advocates approaching computer-based product development as 2 issues
1. design
2. production.

This note examines the issue of *performance*.

# Performance
"Performance" can be divided, broadly, into two categories.

1. Performance during development.
2. Performance in the final app.

The goals of 1 & 2 are vastly different.

In fact the end-user is a different person in both cases.

In (1), we need performance for development turn-around.

In (2) we want performance of the final app.  In other fields, this is called Production 
Engineering.

There is no need to use the same methods (i.e. the same language) for (1) and (2).

Most modern languages aim only for (2) and throw away many considerations for (1).

IMO, there is a confusion about the utility of dynamic vs. static languages.

Dynamic languages - generally - provide better debuggers.  Static languages - generally - throw out debugging in lieue of faster execution and smaller executables.

Attempting to solve both problems with only one language makes the language design problem harder than necessary[^1]. 

[^1]: We need an IDE that allows us to use both kinds of languages.  Q: Do we need a seamless transition between both types of development? Q: How much is that worth?

# (1) Performance For The Developer
In (1) we target performance for the developer.

### Issues
Developer turn-around is the main issue. 

The machine (aka computer) should be used to help the developer.

### Techniques
- elide details to allow better expression of the design
- elide details to allow deeper thinking about the design
- elide details to communicate designs better between team-members
- provide a rich syntax (e.g. text plus diagrams)
- garbage collection
- pipelines
- Worlds
- strong type analysis aimed at DI[^2]
- books: "Design of Everyday Things", "Humane Interface"
- dynamic languages[^4] and REPLs
- automatic inlining & macros (lisp-ish macros)

[^2]: DI means Design Intent
[^4]: Every language can be interpreted.  The emphasis has been on twisting syntax to allow easier compilation.

### Reducing Inconvenience
Development turn-around time can be improved by reducing inconveniences.

Less inconvenience might be provided by:
- declaration after use
- multiple syntaxes
- syntax checking 
- parameter counting
- type checking
- lots of fundamental data types (Rebol and ASON)
- etc.

##### Discussion
###### Declaration After Use
Declaration *before* use is an aid to compiler development and optimization.

In the 1950's, it seemed to be "more efficient" to build one-pass compilers.

The onus, though, has been placed on programmers to declare entities before they are used in the code.  

This affects readability (for human developers) - the "most important" aspects of the design appear at the bottom of a file of code instead of at the top.

This inconvenience could be removed by going back to two-pass compilers (or using JavaScript's "hoisting" ideas).
###### Multiple Syntaxes
See Appendix "Two Syntaxes for Each GPL".

###### Syntax Checking
There exists a tension between language sytax and "syntactic noise".

On one hand, verbose syntax can be easily checked by automated means (i.e. compiler).

On the other hand, verbose syntax makes it harder to "get the big picture" for humans, when maintaining code.

This issue is discussed in the article "Two Syntaxes For Each GPL".

To summarize, it is possible to use PEG technologies to provide more than one syntax for any given language, thereby achieving "the best of both worlds" (a verbose syntax that can be machine-checked, and a concise syntax to aid human understanding).

###### Parameter Counting
A seemingly small detail has come out of more involved research on type checking and type inferencing - simply checking the number of parameters to a function.

This detail is much like the "if ... end if" detail in language syntax design.  It seems trivial but can catch many simple errors effectively and automatically.

Language designers learned this lesson early, but didn't state it explicitly.  

Javascript removed this restriction by allowing uncounted parameter lists.  I assume that the intent was to make the language "more friendly" but had the opposite effect.
###### Type Checking
Type checking was invented as an optimization.  

Type checking allowed one to strip type conversion code from BASIC interpreters (making them run faster).

Type checking and type inferencing has grown, beyond optimization, into a useful tool for thinking about program design.

Many languages inconvenience the programmer by making the programmer explicitly declare types.  

This notational inconvenience can be ameliorated by using PEG-based preprocessors tuned to the problem-at-hand (or, by allowing declaration-after-use).
###### Many Fundamental Types
Sassenrath (inventor of Rebol, which led to the invention of JSON) showed that a *lot* or practical results can be accomplished by providing a rich set of fundamental types, without requiring the programmer to define them explicitly as classes.

Sassenrath is refining his ideas as ASON (see Appendix)[^11].
###### Inlining and Macros
Inlining allows programmers to express code in functional form, and the compiler generates "more efficient" code than pure function calls.

It used to be the case that spotting opportunities for inlining was left up to programmers, e.g. programmers had to insert keywords to mark inlinable functions.

Lisp macros represent inlinable-functions-on-steroids, but, still defined by the programmers.

Compiler technology has developed ways to recognize inlinable functions and to optimize code sequences.

Clearly, one needs to know what one's compiler can and can't do.

If the compiler implements automatic inlining, most code should be written as (inlinable) functions.

Lisp macros differ from C macros in that Lisp macros allow *arbitrary* routines to be called at compile-time and to generate code to be fed to the compiler.

C macros begin at the other end of the spectrum.  C macros are more like Find-and-Replace operations normally found in editors. 

C macros define a different "language" for writing macros.  Lisp macros, OTOH, use the same Lisp language for writing macros.

Ohm (PEG) can provide lisp-like macro preprocessing for any text-based language.

The *m4* macro processor[^41] was designed to provide macro preprocessing that is more powerful than search-and-replace macros.  Tools like *sed* and *awk*, etc., might be used to pre-process code.

Languages that have built-in REGEXP can be used to write macro-like pre-processors.  IMO, PEG is better than REGEXP.

[^41]: found on \*nix.

[^11]: Again, Ohm (a better PEG) could be used to graft these ideas onto existing languages.

# (2) Performance For The Consumer
In (2) we target performance for the consumer.

### Issues

Cost of the final product.

For example, 
- speed
- memory footprint
- cheapest final hardware (e.g. can the app run on a Raspberry Pi, a phone, or, only on the latest hardware?)[^31]

[^31]: I advocate that Optimization be considered and programmed separately, instead of being tangled up with Design.

### Techniques

Various techniques aid in Production Engineering, like 
- parallelism
- caching
- strong type analysis aimed at product performance (allows stripping type checking code from the final product)
- O(n) analysis
- profilers
- C, Rust, C++, etc, etc.
- memory sharing
- time-sharing
- syntactic trade-offs to aid compilation (aka static languages)

# Time To Delivery
Q: What's faster?  Forcing the use of only one language for product realization, or, using more than one language?

Some say that Lisp aids in creating products faster, some say that Rust should be used.[^51]

[^51]: IMO: I would not handcuff myself with Rust.  I advocate (1) creating a Design (i.e. MVP), then (2) optimizing the hell out of the very few places that actually need it.  I want a language that protects me from silly mistakes during (1) and then I want a language that gets out of my way during (2).  If I never have to spend effort on (2), all the better.  The key is to realize that you can't do (1) and (2) at the same time, one or the other suffers.  The biggest "win", IMO, is to allow oneself to create (1) in a concurrent paradigm.

# Architecture, Engineering, Implementation

### Software Architecture
- whiteboards
- sketches
- high-level details
- UX
- extract requirements from end-users, codify requirements

### Software Engineering
Cost-benefit analysis, refactor the Software Architecture to reduce final cost (Q: along which dimension(s)?)
### Software Implementation
Often mis-named engineering (Software Engineering is not Coding, Implementation is Coding).

# Users of Computers

### Business

The programming community addresses the needs of business users, with products like Windows, MacOSX, WYSIWYG word processors, calendars, etc, etc.

### Software Development
Addressing the needs of programing development is mostly stuck in the 1950's - text languages, text editors, GPLs for Software Production Engineering (but no popular languages for Software Architecture).



# How? Using Current Languages

Most current languages are implementation languages, e.g. C++, Rust, Haskell, etc.

GPL (General purpose Programming Languages) are not very general.  They are - typically - aimed mostly at implementation.

E.G. any language that requires the programmer to *define* a data structure is an implementation language (i.e. implementation of the data structure (instead of using a handle to data which is defined elsewhere)).

E.G. any language that supplies low-level operators, like `+`, is an implementation language[^3].

[^3]: The only dataless programming language that I know of is S/SL (not to be confused with SSL).

Why are some developers "better" than other developers?  Discipline, structuring of their designs and implementations. Similarly, some people could write structured assembly programs before HLLs became popular.

Use *shell* pipelines and *\*sh* to construct MVPs.

Note that mapping *\*sh*-based programs to GPL-based programs is not straight-forward, since shell commands are asynchronous and GPLs are mostly synchronous[^6].  See Appendix (Call/Return Spaghetti) for ideas on how to perform such mappings.

PEG parsing[^5] provides a way to create syntax *skins* over existing languages.  Write PEGlets (I call them SCNs) that capture DI and emit different code/languages during development and production.

[^6]: Note that a piepine of functions is *not* the same as a \*nix pipeline
[^5]: My current favorite PEG language is Ohm-JS.  The question of "Why?" is addressed in other notes (see TOC).

# Language Bloat
Creating different languages (better yet: creating IDEs), makes it possible to fine-tune the different languages while eschewing language bloat.

The Handmade Network's manifesto opposes language bloat.  The above begins to address at least some of the issues alluded to in that manifesto.

# Appendix - PEG Applied To WASM
POC for PEG-to-WASM...

[WASM Arithmentic Transpiler](https://guitarvydas.github.io/2021/05/15/WASM-Arithmetic-Transpiler.html)
[WASM Arithmetic github](https://github.com/guitarvydas/arithmetic)

# Appendix - PEG Applied to Transpilation
[PEG vs Other Pattern Matchers](https://guitarvydas.github.io/2021/03/17/PEG-vs.-Other-Pattern-Matchers.html)
(see TOC for further discussion)
# Appendix - PEG Applied to PEG
[Transpilation](https://guitarvydas.github.io/2021/07/12/Transpilation.html)
# Appendix - Two Syntaxes For Each GPL
[Two Syntaxes For Each GPL](https://guitarvydas.github.io/2021/11/14/Two-Syntaxes-For-Each-GPL.html)
# Appendix - Software Development Roles
[Software Development Roles](https://guitarvydas.github.io/2020/12/10/Software-Development-Roles.html)
# Appendix - Call Return Spaghetti
Understanding concurrency.

Breaking CALL/RETURN into separate parts.

This article does not directly show *how* to build concurrent programs, but, if you already know about queues and anonymous functions, it should be a short hop to implementation of true concurrency.

[IMO: Concurrency is a paradigm, not a bag bolted onto the side of a language using  thread libraries.[^21]]

[^21]: See Rob Pike's [Concurrency is not Parallelism](https://www.youtube.com/watch?v=oV9rvDllKEg)

[Call Return Spaghetti](https://guitarvydas.github.io/2020/12/09/CALL-RETURN-Spaghetti.html)

# Appendix - Handmade Manifesto
 [Handmade Manifesto](https://handmade.network/manifesto)

# Appendix - Ohm-JS
[Ohm-JS](https://github.com/harc/ohm)
[Ohm](https://ohmlang.github.io)
[Musings About Ohm-JS](https://guitarvydas.github.io/2021/08/30/Ohm-JS.html)

# Appendix - My Goals
 [Manifesto](https://guitarvydas.github.io/2021/09/23/Manifesto.html)

# Appendix - Worlds
[Worlds Paper Thoughts](https://guitarvydas.github.io/assets/worlds.pdf)
# Appendix - ASON
[ASON](https://altscript.com)
[ASON Ohm-JS parser](https://guitarvydas.github.io/2021/04/10/ASON-Notation-Pipeline.html)
[ASON Tokenizing](https://guitarvydas.github.io/2021/07/07/ASON-Tokenizing.html)
# Appendix - Book: Design of Everyday Things
[Design of Everyday Things](https://en.wikipedia.org/wiki/The_Design_of_Everyday_Things)
# Appendix - Book: The Humane Interface
[The Humane Interface](https://en.wikipedia.org/wiki/The_Humane_Interface)

# Appendix - References
[References](https://guitarvydas.github.io/2021/01/14/References.html)
[TOC as of Sept. 17, 2021](https://guitarvydas.github.io/2021/09/21/Table-of-Contents-Sept-17-2021.html)
# See Also

[Blog](https://guitarvydas.github.io)
[Table of Contents as of Sept 17, 2021](https://guitarvydas.github.io/2021/09/21/Table-of-Contents-Sept-17-2021.html)
[Videos](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy5)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 