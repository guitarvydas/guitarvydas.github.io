---
layout: post
title:  "Brainstorming Due to Thinking About Sector Lisp"
---
- Sector Lisp is a pure version of FP (functional programming)
- O/S (Operating System) processes are *lambda* wannabes 
- Arrays are simply optimized lists - no CDRs
- Sub-dividing memory in a binary form, i.e. 2 sub-divisions (Atom and List, in the case of Sector Lisp) results in anti-code-bloat.

## Implications

### Pure FP

- no allowance for mutation -> small code (less bloat)
- GC is simple

### Processes Are Lambdas

See Greenspun's 10th Rule, if not already familiar with it.

Processes were first implemented in assembler and C.

Lisp implements processes, but calls them LAMBDAs and closures.

First-class functions are LAMBDAs.

### No CDRs

Arrays are simply optimizations of lists, where the CDR is implied.

IIRC this was called "CDR Lists" in early literature.

Non-contiguous cells require special handling, but this need not apply to *all* cells.

Array cells -> Cdr(p) = p + 1

List cells (non-contiguous) -> Cdr(p) = \*(p + 1)

#### String Function Library

String functions are easy to describe in pure FP.

For exampe, *substring* can be written as a combinatino of CAR and CDR applied to Strings (arrays of characters).

String functions become complicated (epicyclic) when mutation is desired. 

Shared memory, memory reuse -> epicycles (code bloat).

### Sub-Dividing Memory in a Binary Fashion

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
