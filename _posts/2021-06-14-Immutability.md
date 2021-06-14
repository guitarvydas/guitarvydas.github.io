---
layout: post
title:  "Immutability"
---

FP emphasizes _immutability_ of data, but the data is only _immutable_ "in the small".  

Data - even in FP - is _mutable_ when the whole system is taken into account.  

For example, imagine how miniKanren operates - it produces an initial match query, then passes the resulting datum on to subsequent queries which transmogrify the datum. 

At the atomic level, it appears that no operation can modify (mutate) the datum.

At a system-level, though, the datum is actually modified, often by appending new information to the datum. 

[Aside: you don't need FP to create this kind of "immutable" data. In other essays, I argue that factbases should only be extended and that facts should not be deleted from factbases.  FBs _acrete_ data, and never delete it.  Deletion of data is only an optimization.]
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
