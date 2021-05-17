---
layout: post
title:  "Refactoring"
---
Refactoring is accidental complexity.

Accidental complexity is also known as "epicycles"[^1].

[^1]: See Copernican vs. Ptolemaic Cosmology.  See Arthur Koestler's "The Sleepwalkers".

The need to refactor a design or to refactor code, should be a red flag. 

Refactoring should never be needed in a design which has been decomposed into its most-atomic units[^2].  
[^2]: Note that I believe that _code_ should be machine-readable.  _Designs_ are meant to be human readable.  Refactoring should be reserved for _designs_ only.  Good designs, don't need to be refactored.  Structure should only be applied to designs, not code.  [At present, all designs are baked into code by virtue of the kinds of languages we use.  If you find a need to refactor code, then split the code into 2 parts - design and code - first.]

Refactoring is accidental complexity caused by too much structure in a design.  

Structure can be added in by creating queries.

Structure should not be baked into a factbase. 

[Structure in queries is OK, structure in factbases is bad].

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
