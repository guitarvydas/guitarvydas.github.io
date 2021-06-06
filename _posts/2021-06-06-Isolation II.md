---
layout: post
title:  "Isolation II"
---

The only thing wrong with mutable state is that it is not isolated. 

Mutable state is not the problem, isolation is the problem.


# Encapsulation

OOP-style encapsulation is not enough.

# UNIX Live Free and Die

UNIX-like processes that die and are automagically cleaned up are a possibility. 

Even lowly C programs running under UNIX are isolated.

[...][^die]

[^die]: Stolen from a license-plate I saw in a UNIX lab. "UNIX Live Free or Die".

# Leaking State
Leaking state should not be allowed.

# Leaking Dependencies
Leaking depedencies should not be allowed.

# Non-Locality

I define non-local as: 
```
Non-locality is: more than an eye-full.
```

Imagine if all code was only 5 lines long.

Imagine if all code was only one window long.

Imagine if all code was only one screen long.

Imagine if all code fit on one piece of paper (i.e. a printed page).

etc. etc.

For example, 26 global variables, named A-Z, are more than I need for only 5 lines of code.

# The Unit of Understandability

7±2.

# Problem: How To Keep Software Units Small?

The problem becomes: how do we keep all software units down to 7±2 lines in length.

# Hierarchy

I favor hierarchy.

Hierarchical variables.

Hierarchical types.

Hierarchical functions.

Hierarchical return values.

Hierarchical parameters.

Hierarchical sub-systems (e.g. a _system_ can be more than 7+-2 lines of code, as long as any sub-unit of code - isolated code - is only 7+-2 lines long).

etc. etc.

_Flat-anything_ is bad.

_Non-fractal_ anything is bad.

# Trees

Trees are hierarchical.

## Graphs and DAGs

Graphs and DAGs are not purely hierarchical, since they allow cross-talk between nodes.


# Libraries of Code

Libraries create dependencies.

Avoid libraries. (!)

Avoid creating and using libraries as we understand them at present.

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
