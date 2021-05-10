---
layout: post
title:  "Software Components 101 - Engine Part 5 Queries"
---


Let's undo one of the human-input conveniences and normalize the factbase to contain only machine-readable codings.

Currently, arrows contain references to graphical objects.  These references should actually be ids.  These reference are (human-readable) synonyms to (machine-readable) ids.

For example, as in part 4, we have facts like:

```
comp(id5, c).
arrow(id40, a41).
arrowBegin(a41, c_c).
arrowEnd(a41, [c_e_m]).
```

Firstly, we can create synonym facts, e.g.
```
comp(id5, c).
synonym(c, id5).
```

Then, we use the synonym facts to modify all arrowBegin facts, e.g.
```
arrowBegin(a41, c_c).
aBegin(a41, idYYY).
```

Then, we use the synonym facts to modify all arrowEnd facts, e.g.
```
arrowEnd(a41, [c_e_m]).
aEnd(a41, [idZZZ]).
```

N.B. Currently, we leave all of the facts in the factbase.  There is no need to remove facts.  Removing facts at this stage -- without proof of needing to do so -- is premature optimization (and uneccessary brain clutter).

We define gobject(ID).  See [q.pl](https://github.com/guitarvydas/basicdasl/blob/master/pseudo/q.pl)

Since we specify the synonym in gobject definitions, the query for synonyms is straight-forward
synonym(ID,Synonym) :-
```
nonArrowGobject(ID,Synonym).
```
[A 'nonArrowGobject' is any gobject except arrows.  See the code for further details.]

Creating a new aBegin fact consists of a compound query - print out an aBegin fact for every arrowBegin fact, replacing the synonym... (again, details elided, see code):
```
printAllABegin :-
    forall(arrowBegin(ID,_),printABegin(ID)).
```

## Sanity Checks ##
I create `gkind` and `tag` queries and double-check by running queries and looking at the diagram (the code for transpilation in this example is meant to be done manually, so I would expect many bugs.  We'll see what I missed when we try to run this stuff.)

For example, we double-check the arrow with two receivers:
```
?- consult(fb).
true.

?- consult(q).
true.

?- printAllAEnd.
...
aEnd(a82,[id62,id69]).
...
false.

?- tag(id62,Tag).
Tag = e_e_l ;
false.
```
(which appears to coincide with what is on the diagram).

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
