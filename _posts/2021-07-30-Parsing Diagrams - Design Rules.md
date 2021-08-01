---
layout: post
title:  "Parsing Diagrams - Design Rules"
---

# Design Rules

Design rules are also known as type checks.

Design rules can be more specific than general type checks.

Design rules relate to the solution instead of being generalized to handle many possibilities.

As an example, we have written a design rule that checks for orphan ports.  Ports that are not contained within any rectangle are flagged as errors.

The essence of a design rule that checks for orphans is:

```
orphanport(ID):-
    ellipse(ID,_),
    \+ contains(_,ID).
```

(i.e. any ellipse that is not contained by a diagram object is an orphan).

The rest of the code prints error messages and appeases PROLOG:

```
:- dynamic contains/2.
orphanport(ID):-
    ellipse(ID,_),
    \+ contains(_,ID).

printOrphans:-
    bagof(E,orphanport(E),B),
    printOrphan(B).
printOrphans.


printOrphan([]).
printOrphan([H|T]):-
    format("Design Rule FATAL Error: orphan port ~w~n", H),
    printOrphan(T).
```

# Rundesignrule.bash

A *bash* script runs this design rule and exits if the word `FATAL` is in the output.

The bash script is run by the main bash script `run.bash`.

```
#!/bin/bash

swipl -g 'consult(fb).' \
      -g 'consult(designrule).' \
      -g 'printOrphans.' \
      -g 'halt.' \
      > errors.txt
if grep 'FATAL' errors.txt
then
    echo quitting
    exit 1
fi

```



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
