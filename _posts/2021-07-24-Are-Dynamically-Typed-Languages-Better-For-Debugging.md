---
layout: post
title:  "Are Dynamically-Typed Languages Better For Debugging?"
---

Theoretically, debuggers for statically typed languages should be equal to debuggers for dynamically-typed languages.

Historically, though, dynamic languages are easier to debug. 

Program development breaks down, roughly, into two aspects

1. getting the requirements right, and,
2. mapping the requirements to code.

Strong typing is aimed at solving (2), but (1) is still done in a mostly ad-hoc manner (strong typing helps with *thinking about* (1), but does not solve (1)).

Debugging can be helpful in iterating designs as needed by (1) and continues to be an important tool in Designers' toolbelts.

# REPL

REPL means Read-Eval-Print-Loop.

The REPL concept was invented using dynamically-typed languages (Lisp).

In a REPL, the full language is exposed to the programmer.  

REPL commands are indistinguishable from the language itself.  

One doesn't need to learn a new language for debugging.

# Debugger DSL

The "language" used to enter debugger commands is a DSL, but, not often thought-of that way.

For example, Lisp can be used in a Lisp REPL.  Lisp is the language *and* Lisp is the debugger DSL.

On the other hand, *gdb* can be used to debug C.  C is the language, but the debugger DSL is some other language, i.e. not C.

The ideal situation is to be able to use the same language for programming and for debugging.

# History - We Have Always Done It This Way

Historically, we have built debuggers separately from language compilers/interpreters.

The *reason* for doing this is optimization.

The hardware of yesteryear was not capable of running statically-typed languages as debugger DSLs.

And, it was thought that debuggers were not as important as the languages themselves.

# Creating REPLs For Statically Typed Languages

The answer to creation of debuggers for statically typed languages is quite simple

a) build the whole language (compiler) *into* the REPL

b) have the compiler leave enough information lying around for the REPL

- typical compilers destroy information, such as scoping and variable names
- such information must be retained[^retain]
- the debugger/REPL must display data in a way that mimics the definition of data in the language -being-debugged
- the debugger/REPL must accept commands that appear to be written in the language-being-debugged.

# Lisp

Lisp is thought of as an interpreted language, but has (long ago) graduated to being a compiled language.

Modern Lisps tend to run the full compiler in the REPL, as needed in point (a).

Modern Lisps tend to compile *all* code, even code typed in at the REPL.

When a programmer inserts breakpoints into code, Lisps tend to recompile the code into interpreted form for easier debugging.

[^retain]: This is actually done by many compilers of today. When one invokes the the HTML/JS console in a web browser, there is usually enough information available to the debugger to show data frames in an understandable manner.

# Static Typing vs. Dynamic Typing

Static typing is a subset of dynamic typing.

Any fully-typed language checks the types of all of the program constituents.

Static type checkers are arranged to do this checking *before* the code in question runs.  

Dynamic type checkers do the same checking, but at runtime.

Dynamically typed languages are often conflated with languages that are not strongly typed, but *dynamic typing* is actually the *same* as *static typing*, just done at a different time.

# Interpretation

Any strongly typed language *can* be interpreted.

Any statically typed, strongly typed language can be, both, compiled and interpreted.

A compiler merely creates a minimized form of the code, and removes the need for runtime type-checking.

Corrolary: a compiler is an interpreter.

An interpreter is useful as a REPL.

Every language should come with a

- compiler, and
- an interpreter.

# Compilation

Compilation is an optimization.

Compilation is nice-to-have, but not necessary.

Compilation makes the final app run faster/smaller.

# History, Again

Historically, building compilers and interpreters has taken a long time (years, each).

Languages that were knocked-off in a week, say JavaScript, took many more years to hone (witness the succession of versions of the language).

Historically, it was considered "enough" to build only a compiler or to build only an interpreter for a language.

# An Interpreter And Compiler For Every Language

We have more efficient hardware now.

We have better language-building tools now.

We *should* demand that every language have a compiler *and* an interpreter out of the chute.  They should be provably the same and give decent error messages[^error] (at least the interpreter should do so). 

An interpreter should be considered to be most important, a compiler is but an optimization.  Some languages cannot be compiled and, hence, only provide an interpreter.

Corrolary: _Every language must have an interpreter. If the language has a compiler, too, that should be considered to be a bonus._

[^error]: A stack backtrace is not an error message.  It is a core dump.
[^]: 

# See Also

[Failure Driven Development](https://guitarvydas.github.io/2021/04/23/Failure-Driven-Design.html)

[Homoiconicity](https://en.wikipedia.org/wiki/Homoiconicity)

[Triples](https://guitarvydas.github.io/2021/03/16/Triples.html)

[Triples and Factbases](https://guitarvydas.github.io/2021/01/17/Factbases.html)

[Toolbox Languages](https://guitarvydas.github.io/2021/03/16/Toolbox-Languages.html)

[Toolbox Languages 2](https://guitarvydas.github.io/2021/04/28/Toolbox-Languages-(2).html)

essay on Low Friction Design

essay on Agile

essay on UML

[Lisp](https://guitarvydas.github.io/2021/07/26/Lisp.html)

[Blog](https://guitarvydas.github.io)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 