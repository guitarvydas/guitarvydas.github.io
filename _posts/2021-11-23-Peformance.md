
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

Most modern languages aim only for (2) and throw out many considerations for (1).

IMO, there is a confusion about the utility of dynamic vs. static languages.

Dynamic languages - generally - provide better debuggers.  Static languages - generally - throw out debugging in lieue of faster execution and smaller executables.

Attempting to solve both problems with only one language makes the language design problem harder than necessary[^1]. 

[^1]: We need an IDE that allows us to use both kinds of languages.  Q: Do we need a seamless transition between both types of development? Q: How much is that worth?

# (1) Performance For The Developer
In (1) we target performance for the developer.

### Issues
Developer turn-around is the main issue. 

Use the machine (aka computer) to help the developer.

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

[^2]: DI means Design Intent
[^4]: Every language can be interpreted.  The emphasis has been on twisting syntax to allow easier compilation.

# (2) Performance For The Consumer
In (2) we target performance for the consumer.

### Issues

Cost of the final product.

For example, 
- speed
- memory footprint
- cheapest final hardware (e.g. can the app run on a Raspberry Pi, a phone, or, the latest MacBook?)

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
Q: What's faster?  Forcing the use of only one language for product realization vs. using more than one language?

Some say that Lisp aids in creating products faster, some say that Rust should be used.

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
Addressing the needs of programing development is mostly stuck in the 1950's - text languages, text editors, GPLs for Software Production Engineering (but not Software Architecture).



# How? Using Current Languages

Most current languages are implementation languages, e.g. C++, Rust, Haskell, etc.

GPL (General purpose Programming Languages) are not very general.  They are - typically - aimed mostly at implementation.

E.G. any language that requires the programmer to *define* a data structure is an implementation language (implementation of the data structure).

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

# Appendix - PEG Applied To WASM
POC for PEG-to-WASM...

[WASM Arithmentic Transpiler](https://guitarvydas.github.io/2021/05/15/WASM-Arithmetic-Transpiler.html)
[WASM Arithmetic github[(https://github.com/guitarvydas/arithmetic)

# Appendix - PEG Applied to Transpilation
[PEG vs Other Pattern Matchers](https://guitarvydas.github.io/2021/03/17/PEG-vs.-Other-Pattern-Matchers.html)
(see TOC for further discussion)
# Appendix - PEG Applied to PEG
https://guitarvydas.github.io/2021/07/12/Transpilation.html
# Appendix - Two Syntaxes For Every Language
[Two Syntaxes For Every GPL](https://guitarvydas.github.io/2021/11/14/Two-Syntaxes-For-Each-GPL.html)
# Appendix - Software Development Roles
[Software Development Roles](https://guitarvydas.github.io/2020/12/10/Software-Development-Roles.html)
# Appendix - Call Return Spaghetti
Understanding concurrency.

Breaking CALL/RETURN into separate parts.

[Call Return Spaghetti](https://guitarvydas.github.io/2020/12/09/CALL-RETURN-Spaghetti.html

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

# Appendix - References
[References](https://guitarvydas.github.io/2021/01/14/References.html)
[TOC as of Sept. 17, 2021](https://guitarvydas.github.io/2021/09/21/Table-of-Contents-Sept-17-2021.html)