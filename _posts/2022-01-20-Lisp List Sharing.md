---
layout: post
title:  "Lisp List Sharing"
---

Lisp lists are more efficient than OO lists

Lisp lists share structure by allowing multiple CDRs to point to the same cell.

To tack a cell onto the front of a list, mutation is not required, simply CONS a cell whose CDR points to a "shared" list and call a function with that new CONS as an arg.

For example, if you have a list (B C), you can make 2 new lists (A B C) and (D B C) by CONS(A, (B C)) and CONS(D, (B C)).

![List Sharing](Lisp-1-Sharing.svg)
![Recursion](Lisp-2-Recursion.svg)
![CDRing Down A List](Lisp-3-CDRing.svg)
![TCO (Tail Call Optimization)](Lisp-4-TCO.svg)
# See Also

[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 