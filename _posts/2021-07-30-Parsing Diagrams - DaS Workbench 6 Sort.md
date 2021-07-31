---
layout: post
title:  "Parsing Diagrams - DaS Workbench 5 Factbase Emitter"
---

# Sort

This phase performs a simple alphabetic sort to appease PROLOG.

PROLOG requires that facts be grouped together.  Alphabetic sorting is not required, but is easy to perform and creates an acceptable grouping.

[_In fact, modern PROLOG engines allow un-grouped facts.  This requires a bit of extra syntax. It would have been possible to leave the factbase un-grouped, but, the object of this set of essays is to show that it is easy to compose pipelines of grok/emit phases, so we chose to insert this simple sorting phase._]

This phase simply accepts the input (the result of the preceding phase) and calls JS `sort()` to produce the final output string.

![2021-07-30 sort.png](https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-07-30%20sort.png?raw=true)

[_This is probably something a Production Engineer would attack early, but, in Software Architecture, we strive for obvious-ness instead of machine-level efficiency.  Again, the use of a grok/emit pipeline makes it easy to construct architectures without worrying about fine-grained details._]

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
