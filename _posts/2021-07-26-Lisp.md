---
layout: post
title:  "Lisp"
---

# Lisp

Lisp is an expression language.  Every statement returns a value.

Lisp is machine-readable.  

Lisp's RPN notation is a tree notation.

Lisp is programmed using parse trees (often called ASTs and CSTs[^ast]).  

I would argue that Lisp has no syntax.  

Lisp represents programs as Lists (not characters).This feature makes it especially easy to write REPLs for Lisp in Lisp, since Lisp contains many features for editing Lists.  This feature is called *homoiconicity*.

Lisp *sexps* are much like triples.

The Lisp language contains many features aimed at debugging, for example *restarts*, the *break* statement, etc.

Lisp macros are List-manipulation functions that produce source code (lists) that are fed into the Lisp compiler.

# Common Lisp

Common Lisp is a standard and was created as the union of several popular Lisps.

# Racket

Racket is a variant of Lisp (based on Scheme, itself a variant of Lisp) that provides an IDE and various syntaxes (#lang).

# Example - Editing A Program

A simple and meaningless example of editing a program.

Changing 1+1 to 1-1.

![2021-07-26-Lisp Example.png](https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-07-26-Lisp%20Example.png?raw=true)

[_Obviously, the rewriting operation is verbose.  Lispers use a different syntactic sugaring for doing such rewrites._]

[^ast]: AST means Abstract Syntax Tree.  CST means Concrete Syntax Tree.  A grammar defines an AST.  A parser produces a CST.

# See Also

[Blog](https://guitarvydas.github.io)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
