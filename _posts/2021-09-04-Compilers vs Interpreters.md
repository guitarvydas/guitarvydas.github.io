---
layout: post
title:  "Compilers vs. Interpreters"
---
Every interpreter interprets some data structure.

If the interpreter interprets a tree data structure, it is a tree-walk interpreter.

Originally, interpreters interpreted source code as strings.

Strings are considered to be "inefficient", since they are usually variable length. CPU power is required to parse (and re-parse) the variable-length strings.

Language designers tried to improve machine runtime efficiency by reading the strings only once, storing info into hash tables, and then compiling the source code into  bytecodes (a linear array of bytes -- a data structure -- without the need to re-scan strings).

This technique was later re-branded as VM's (virtual machines).

A CPU chip is an interpreter (!).  A CPU interprets opcodes (stored as words in memory) and hides the details of what is really going on underneath.  CPU chips are implemented using various forms of rust (oxides).

Software people tend to draw a line between interpreters of opcodes vs. interpreters of other kinds of data structures (which, of course, are interpreted by the CPU interpreter hardware).

Programmers tend to think in terms of
1. compilation -- to some convenient data structure, such as CPU opcodes
2. interpretation -- of some data structure.

The thing that programmers call interpreters are usually scripts that boil down to CPU opcodes.  The inefficiency of software-interpreters is that they use scripts of CPU opcodes to parse and evaluate data structures built on top of CPU opcodes.  You get towers of data structures which boil down to oxides.  "Efficiency" comes from removing as many levels from the towers as possible before running the oxide-based interpreter.

Compilers remove some of the runtime overhead of interpretation before running an app on a CPU (which is an interpreter, itself).

# JIT

JIT is considered to be a compiler.

JIT interprets the input source only once and compiles that source to opcodes on-the-fly.

Traditional compilers compile all of the source code before-hand.  JIT compilers compile the souce code in snippets, on-the-fly -- as the code is encountered.  One of the advantages of JIT is that it doesn't need to waste time compiling code snippets that aren't encountered when the app is run.

JIT was originally explored in Lisp (fast-calls).

Java popularized JIT (as well as garbage collection, as well as OOP, etc.).

In fact, the language Self, explored JIT which then made its way into Java.

# Compilers Are Optimizations

The things we call _compilers_ are merely optimizations of language interpreters.

Imagine that _every_ language starts out in interpreted form.

_Compilers_ are just sets of optimizations to those interpreted forms.

The _optimizations_ consist of mutations to the languages that allow the languages to be pre-interpreted.  [_Not all languages lend themselves to pre-interpretation. The programming community has discovered what language features aid pre-interpretation (e.g. type systems).  This can be likened to how the programming community discovered what language features aided syntax checking (e.g. `end if` vs. `}`)_]

The pre-interpretation step calculates various properties of the languages, e.g.
1. Syntax checking.
2. Type checking.

The pre-interpreters perform the checks once for each application, then delete portions of the applications, allowing the runtime-interpreters to run more quickly and to use less storage.

The assumption is that pre-interpretation will be executed much less frequently than the runtime-interpretation of the applications.

Pre-checking various parts of the applications _should_ result in more efficient operation of the pruned applications.

The pre-interpreters are called _compilers_.

# OOP -- Classes vs. Prototypes

Class-based OOP is an optimized version of prototype-based OOP.

Classes allow for easier pre-interpretation of programs. Programs based on prototype-based OOP are harder to pre-interpret.

# Typing
## Static Types vs. Dynamic Types

Most modern GPLs, focus on static type systems as an aid to pre-interpretation.

Dynamically-typed languages, such as early Lisps (before Common Lisp), focused on full type-checking that was done at runtime, but was difficult to pre-interpret.

It turns out that static typing allows the pre-interpreter to create faster/smaller code.

Type-checking at runtime does not mean that the languages are untyped.

Type-checking at runtime usually implies that extra time/space is expended at runtime to determine the types of data, each time the data is encountered.

One of the _optimizations_ consists of annotating data in a way that allows the pre-interpreter to check consistency and to discard runtime checks.  This kind of _optimization_ is called _type checking_.

## Typed language vs. Untyped Languages

Some languages are loosely-typed or completely untyped.

These languages allow implicit coercion between very disparate types of data (e.g. strings vs. numbers) at runtime. Coercions are usually done "under the hood" by the interpreters, taking the burden of annotating data off of programmers.

Type annotations usually involve extra code size and verbiage.

# Type Systems as Design Aids

Many programmers feel that type systems allow them to design programs "correctly".

This is the same effect as when HLLs[^1] introduced syntax checking vs. ad-hoc assembler code.

[^1:] HLL means High-Level Language.

`Structured Programming` brought ordering and encapsulation to syntax, reducing the ad-hoc nature of code even more.

`Locality of Reference` further tightened code and removed particular kinds of ad-hoc code (e.g. global vs. local variables).

Type annotations (and type inferencing) provide more details that allow the pre-interpreters to weed out larger classes of programming errors.

The cost of type annotations is borne by the programmers using the typed languages, in the form of more text and more details and more (explicit) precision. 

Type inferencing is an attempt to reduce the cognitive load on programmers.

Type checking can automatically check for a wider class of programming errors, but, at this time, cannot check that a program "does what the customer wants".  Type checking can, at best, check that a program "does what the programmer wants", which is not always the same as checking against customers' desires and requirements.

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
