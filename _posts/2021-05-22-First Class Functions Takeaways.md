---
layout: post
title:  "First Class Functions - Takeaways"
---

# GOTO

First Class Functions are GOTOs.

CPS - Continuation Passing Style - is GOTOs on steroids.

GOTOs first appeared in Assembly language.

CPS was borne out of /CC functions in Scheme.

# Utility

First Class functions & CPS are very useful in Denotational Semantics (to express control-flow).

Otherwise, 1st class functions and CPS should not be used in lieue of more structured versions.  What are these more structured versions?  "GOTO Considered Harmful" might provide clues.

Current usage of 1st class functions is Structured only because of the severe restrictions imposed by FP - one-in, one-out[^exceptions] model of computing (aka "synchronous calculator").

[^exceptions]: Exceptions are but warts, bags on the side of one-in/one-out syntax. 

# Lambdas

Lambdas first appeared in Lisp (approx. 1956) based on lambda calculus.

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
