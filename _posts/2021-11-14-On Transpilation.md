---
layout: post
title:  "On Transpilers"
---
# Transpilers
I now use Ohm-JS to define small *transpilers* and used a *toolbox language*, like Common Lisp, Javascript, etc., to do all of the heavy lifting for me.

I don't write code to implement scanners.  I use PEG (I used to used regular expressions).

I don't write code to implement parsers.  I use PEG[^1].

[^1]: I like the Ohm language (based on PEG).  I regularly use [Ohm-JS](https://github.com/harc/ohm) and [Ohm-Editor](https://ohmlang.github.io/editor/).

I don't write code to do syntax-checking.  I use a parser.

I don't write code to implement semantics checking.  I use the underlying *toolbox language* to do most of the work for me (e.g. hash tables, etc.[^2]).

[^2]: Semantic analysis (type checking) consists, at a base level, of storing some information and retrieving that information.  More complicated type checking consists of inferring type information, which, itself, decomposes into two broad categories - (1) *what* to infer, and, (2) *how* to infer it. Akin to the use of `end if` -like constructs in parsing, there are some simple - low-hanging-fruit - type checks that can be performed fairly easily with information stored in tables.

I don't write code to implement code emission.  I transpile[^3] to some base language, e.g. JavaScript, and let the corresponding compiler do the work for me.

[^3]: Transpilation is source-to-source compilation.  Compile one source language to another textual language. 

I don't write code to implement code optimization.  I transpile to some base language and let the corresponding compiler do the work for me.
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