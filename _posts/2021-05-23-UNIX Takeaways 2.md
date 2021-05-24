---
layout: post
title:  "UNIX Takeaways 2"
---

- restricted interfaces
- low-level types for interfaces

# Restricted Interfaces

UNIX commands have
- 1 input (stdin)
- 2 outputs (stdout, stderr).

UNIX shows how much can be done with simple interfaces.

# Low-Level Types
Typing should be done in layers, not in an _all-in-one_ basis.

UNIX commands use a very simple, low-level type for communication between components - a line of text.

This simplicity allows components to be plugged together.

Note that more elaborate types can be used, but the fundamental (atomic) type for plugging components together remains constant (a line of text).

More elaborate types can be enforced by components in UNIX pipelines.

# Type Pipelines
More elaborate types can be checked in layers in a type pipeline.  Each successive component in a pipeline either 
1. passes data down the pipe (after checking it)
2. signals an error, e.g. by withholding (1) and sending an error object (/message) on a side-channel.

This structure inherently needs multiple outputs (e.g. at least stdout and stderr (I favor having more than 2)) which is not well-served by functional notation (which is fundamentally a 1-in-1-out notation[^bags])

[^bags]: Over time, the limits of functional notation have been addressed by playing whack-a-mole - adding bags onto the side of the otherwise-pure syntax, e.g. exceptions.

# FBP

FBP means Flow-Based Programming.

UNIX commands are a subset of FBP[^cbp].

[^cbp]: I favor Component Based Programming, which is more similar to EE and LEGO.  FBP focuses on the flows of data while CBP focuses on the components themselves.

# Edge-Cases

Q: What kinds of operations cannot be handled with the above?

Q: Should we create PLs[^pl] that are the Union of all edge-cases, or, should we create many SCNs[^scn] instead?  

Q: Does PEG offer advantages over REGEX for creating commands (e.g. grep vs. fictional peggrep ; awk vs. fictional pegawk ; python vs. fictional pegpy ; lisp vs. peglisp)?  Is this an edge-case or something common to many apps?

Q: Should PLs be hierarchical, not flat?  Should variables be hierarchical?  (Symbols, in general).  [Example: "y = mx + b" vs. "y = (slope * x) + intersect".  Is the difference a language decision or a IDE feature?  Or, is this the goal of Projectional Editing?).]

[^scn]: SCN means Solution Centric Notation (essentially a light-weight DSL).
[^pl]: PL means Programming Language.

# See Also

https://guitarvydas.github.io/2021/01/14/References.html
https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html
  

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
