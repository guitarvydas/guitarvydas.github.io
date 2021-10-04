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

*All* languages can be interpreted.

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

[^1]: The REPL happened to be a Lisp REPL, but that is beside the point of this article.  I think that pre-CL Lisp was easier to debug than Common Lisp.

# See Also

[Blog](https://guitarvydas.github.io)
[Table of Contents](https://guitarvydas.github.io/2021/09/21/Table-of-Contents-Sept-17-2021.html)
[Videos](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy5)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
