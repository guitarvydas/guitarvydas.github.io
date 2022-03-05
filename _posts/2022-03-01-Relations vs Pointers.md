---
layout: post

title: "Relations vs. Pointers"

---

The relation

`contains(rect, circle)`

usually implemented as a pointer from rect -> circle (and, maybe, circle -> rect, or both).

Such pointers are relations.  They can be represented as relations:

```
contains(rect,circle).
containedby(circle,rect).
```

Information is not lost in the relational representation.

Information is *flatttened* to its simplest form - a *relation*.

Persisting information in flattened form is more flexible, but, if you want to (re-)structure the data, it takes work (CPU).  

With modern hardware, this extra work is inexpensive.  The reconstruction work happens quickly and uses cheap memory.

Machine time is inexpensive.

Machines (computers) can perform repetitive work flawlessly.

Flexibility equates to savings of architecting time (human time, programming time).

Destruction of flexibility is an optimization and should be used sparingly.  

On modern hardware, optimization is not needed in most use-cases.

Destruction of flexibility also tends to destroy DI.  Optimization conflates architectural concerns with optimization concerns.  This tends to obfuscate DI. This affects understandability and, therefore, affects maintenance.

Unnecessary optimization is a bad idea.

The plus operator `+` is an optimization of the plus function `plus()`.  Any language that provides a `+` operator is - at least psychologically - encouraging optimization in preference to DI.

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