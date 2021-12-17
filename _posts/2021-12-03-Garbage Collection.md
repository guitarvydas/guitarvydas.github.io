---
layout: post
title:  "Garbage Collection"
---

# Garbage Collection is an Implementation Detail
Garbage collection is necessary only if memory is re-used.  

Re-use of memory is an optimization, hence, GC (Garbage Collection) is a memory optimization detail.

At the *DI*[^2] level (aka Software Architecture), there should be no consideration of memory re-use. 

DI expresses the Design of a Solution, and, does not delve into details, such as memory re-use.

[^2]: DI means Design Intent.


# Memory Re-Use
Re-use of memory has caused many *accidental complexities*.  

Memory re-use might be a necessary evil for constructing systems using present computer hardware, but, this detail - memory re-use - should not be tangled up in DI.

Tangling Production Engineering concepts with DI results in Spaghetti Design.

# The Best Garbage Collector, The 2nd-Best GC, The 3rd-Best GC, etc.
The best garbage collector is: no garbage collector.

The second-best garbage collector is: the biblical flood, wipe the slate clean[^1].

[^1]: The Unix process model uses the biblical flood method.  When a process dies, the Dispatcher wipes the slate (the memory) clean and re-uses the memory for other processes.

The third-best garbage-collector is: anything that impinges on the running code, e.g. the Lisp GC, the Smalltalk GC, the Java GC, the Rust ownership model, reference-counting, etc., etc.

Memory is now cheap.  Why bother reclaiming it?  

# Servers Run Forever
Servers are meant to `run forever`.

Rhetorical question: what does that mean to GC?  

Rhetorical question: should every app pay to have run-forever-style GC?

# Appendix - See Also

[Blog](https://guitarvydas.github.io)
[Table of Contents as of Dec. 01, 2021](https://guitarvydas.github.io/2021/12/01/Table-of-Contents-December-01-2021.html)
[Videos](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy5)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
