---
layout: post
title:  "Two Parts of Mathematics"
---
Mathematics consists of 2 main parts:
1. the mechanics of manipulating symbols
2. the hard-won knowledge of what works and what doesn't (algorithms, laws, principles, etc.).

Part 1 is simple text manipulation.

Mathematics was invented when the only tools were pen and paper.

The UNIX people *almost* got part 1 by producing a set of utilities for manipulating symbols in the form of text. 

The "problem" with the UNIX notation was that text was only text up to end-of-line.  

Newline is *special* in UNIX

Lisp *almost* got part 1, except that the symbols must be arranged as lists (CONS cells).

# New Math Manipulation
We need a way to manipulate symbols in a way that doesn't make newlines and CONS cells special.

Computers like to think in terms of bytes.

# PEG

How can we manipulate raw bytes?

Parsers.

PEG parsing makes parsing easier.  

PEG is a DSL for parsing.

Ohm-JS is improved PEG.

# Diagrams
Why stop at characters?

We can manipulate diagrams using computers.

How can we draw diagrams and then manipulate them?

A beginning might be:
- draw.io
- SVG
- d2f.

# See Also
[d2f - Diagram to Text Converter](https://guitarvydas.github.io/2022/01/14/D2F.html)
[Ohm-JS](https://www.npmjs.com/package/ohm-js) (see, also, my articles on PEG and Ohm-JS)
[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 