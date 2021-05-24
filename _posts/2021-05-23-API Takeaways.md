---
layout: post
title:  "API Takeaways"
---
- restricted interface between components

# Input APIs
APIs usually specify only the input side of software components.

# Output APIs
Full APIs must include, both, input and output descriptions.

# DLLs
DLLs - .dll, .so, .dylib files - are one form of output API (created using indirection which is resolved by the linker).

DLLs are not formalized to the point of having first-class output APIs.

# Normalized Interfaces, APIs

Input APIs and output APIs should look the same.

Currently we specify output APIs using a mish-mosh of syntax, e.g. exceptions, synchronous return values, etc.

# Components

A Component is described by
- a name
- an input interface
- an output interface.

[N.B. Currently, we specify APIs with too much detail, a result of flatness instead of layering.  Libraries are hard to use because of the fact that too much detail is exposed at the top levels].

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
