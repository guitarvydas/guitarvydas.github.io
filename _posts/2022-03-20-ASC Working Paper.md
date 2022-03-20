---
layout: post
title:  "ASC Working Paper (March 20, 2022)"
---
## Goals
1. Define ASC syntax.
2. Transpile ASC to alist form (in Lisp, in Python, etc.)
3. Produce example diagram->concurrentLambda code
4. Intermediate tools.

ASC means "Asynchronous Software Component".

## Status
### 1. Define ASC Syntax
First cut done.  See `lookup.asc`. (below)
### 2. Transpile ASC
Working on this, see section 2.0 below.
### 3. Produce Example
First cut done and working. Hand-compiled from lookup.drawio to lookup.lisp.

### 4. Intermediate Tools
#### Prep
Done[^done]. [Prep](https://github.com/guitarvydas/prep)
#### DaS To Python
Done. [DaS](https://github.com/guitarvydas/das)

[^done]: "Done" in this context means "experimentally usable".  Not necessarily production quality.  I would be happy to transfer this stuff to maintainers.

## More Details
## 1.0 ASC Syntax
[lookup.asc](https://github.com/guitarvydas/dasl2/blob/dev/asca/lookup.asca)
## 2.0 Transpile ASC
working in [asca working directory](https://github.com/guitarvydas/dasl2/tree/dev/asca)

see Makefile, `make dev`

goal: transpile asc "assembler" to lisp [lookup.asc](https://github.com/guitarvydas/dasl2/blob/dev/asca/lookup.asca)to something like [lookup.proto.lisp](https://github.com/guitarvydas/dasl2/blob/dev/lisp/lookup.proto.lisp)

### sub-goal 
- tokenize lookup.asca to lookup.asct
- [working on this] write Ohm-JS grammar to parse tokens
- [future] write .fmt file to output .lisp, .py, etc. alists
## 3.0 Produce Example of Concurrent Lambdas
see working paper `2022-03-20-Concurrent Lambdas`.

## See Also

[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)
[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC9EJr0nKHwadbHUtc5zHdmQ/videos)
[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Books](https://leanpub.com/u/paul-tarvydas.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 