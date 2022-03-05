---
layout: post
title:  "Debuggers"
---
# REPL

The "best" debugger I used was a REPL[^1].

REPL means "Read, Eval, Print, Loop".  

Debugging in a REPL uses the language, itself, as the syntax for the debugger.

Once inside a REPL, a programmer can query (and change) the state of a computation using familiar syntax.

# Interpretation vs. Compilation

*All* programming languages can be interpreted.

Only *some* languages can be compiled.

Compilation is an optimization, often applied prematurely.

# Interpreter and REPL For All Languages Before Compilers

IMO, *all* programming languages should start out life as interpreters with REPLs.

Then, and only then, compilers can be built (for some languages / language features).

# Debugging Workflow

The workflow could be changed to:

1. write the program
2. debug the program in the REPL
3. compile the debugged program for production.

# How To Build Interpreters For Existing Languages?

## Ohm-JS?

Q: Can Ohm-JS (+ CL, Pyton, etc.) be used to build interpreters for all existing compile-only languages?

## Denotational Semantics?

Q: Can Denotational Semantics produce interpreters for languages and tie compilers back to the original language semantics?  Can the Denotational Semantics of a language be used to produce, both, the interpreter and the compiler?

[^1]: The REPL happened to be a Lisp REPL, but that is beside the point of this article.  I think that pre-CL Lisp was easier to debug than is Common Lisp. OTOH Lispworks (for CL) defines what a debugger should be capable of.

# See Also
[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)
[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC9EJr0nKHwadbHUtc5zHdmQ/videos)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
