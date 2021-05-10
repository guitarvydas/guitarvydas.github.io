---
layout: post
title:  "Software Component 101 - Part 4 Review"
---
In beginning to work on part 5 of this series of essays, I noticed a design bug.

Arrows contain two parts (`arrowBegin` and `arrowEnd`) and should be written as a pair referencing the containing composite component.

For example
```
  <outline text="comp “c”">
  ...
    <outline text="arrow c/c  c/e/m" />
  ...
```

should create a pair, referring to "comp c", and, should create a beginning and end for the pair, like...
```
comp(id5, c).
arrow(id5,idXXX).
arrowBegin(idXXX,c_c).
arrowEnd(idXXX,[c_c_m]).
```

(In part 5, we will convert the synonyms `"c_c"` and `"c_c_m"` into ids.  This essay is only about fixing the design bug mentioned above).

This bug should be relatively easy to repair.  We need to visit the `grasem`/`glue` code for arrow and add another fact.

[N.B. There is at least one other appeasement of human-readability - the use of PROLOG lists ([...]) in arrowEnd facts.  I don't think that we'll bother to fix this.  The pure form would be to unroll arrowEnd and make it into multiple facts, i.e. to express the Lists as multiple facts (somehting like beginArrowEnd, arrowEndNext, arrowEndEnd). PROLOG lets us "get away" with lists of the form [ ... ] and we will let this impurity stand, for now.  This is an interim project which doesn't need to be fixed yet (YAGNI)].
