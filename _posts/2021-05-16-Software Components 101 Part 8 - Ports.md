---
layout: post
title:  "Software Components 101 Part 8 - Ports"
---
We proceed by making various Port queries.

External ports are circles.

Internal ports are rectangles.

Input ports are green.

Implicit ports have stroke-width=3 

All ports with a different stroke-width will be considered to be explicit Ports.

Do we write this information out to a new factbase, or, do we, in true PROLOG tradision, just keep the queries as queries in future code ("all-in-one")?

The answer depends on the _Responsibility of the Architect_ - to make the design clear to all readers of the code.

As the Architect in this case, I think of Ports as a "chunk" of the design.  This leads me writing new facts out, so that future readers can deal with the same chunks that I used during design.  Other Architects might make other choices.

Leaving a soup of queries is, IMO, cruel and results, ultimately, in spaghetti design.  It is better to chunk now and let future readers un-chunk the design.  This would be akin to _refactoring_ the design.  

A design which is _too simple_ is better, IMO.   

Once a design has been spaghetti-fied by joining unrelated chunks into one blob, it becomes harder to understand and to refactor.[^refactor]

[^refactor]: In fact, the need to refactor a design or to refactor code, should be a red flag.  Refactoring should never be needed in a design which has been decomposed into its most-atomic units.  In other words: refactoring is an epicycle (accidental complexity) caused by too much structure in a design.  Structure can be added in by creating queries ; structure should not be baked into a factbase. (Structure in queries is OK, structure in factbases is bad).

## Added queries:
```
externalPort(C) :-
    circle(C,_).
internalPort(R) :-
    rect(R,_),
    \+ comp(R,_).
port(P):-
    externalPort(P).
port(P):-
    internalPort(P).
inputPort(P) :-
    port(P).
outputPort(P):-
    port(P),
    \+ inputPort(P).
implicitPort(P):-
    port(P),
    strokeWidth(P,3).
explicitPort(P):-
    port(P),
    \+ implicitPort(P).
describePort(P):-
    port(P),
    format("port(~w,nil).~n", [P]),
    describeLocation(P),
    describeDirection(P),
    describeConnectionType(P).
describeLocation(P) :-
    externalPort(P),
    format("location(~w,external).~n", P).
describeLocation(P) :-
    internalPort(P),
    format("location(~w,internal).~n", P).
describeDirection(P) :-
    inputPort(P),
    format("direction(~w,input).~n", P).
describeDirection(P) :-
    outputPort(P),
    format("direction(~w,output).~n", P).
describeConnectionType(P) :-
    explicitPort(P),
    format("connectionType(~w,explicit).~n", P).
describeConnectionType(P) :-
    implicitPort(P),
    format("connectionType(~w,implicit).~n", P).
describeAllPorts:-
    setof(P,describePort(P),_).
```
## Query
```
?- consult(fb).
true.

?- consult(q).
true.

?- describeAllPorts.
port(id10,nil).
location(id10,external).
direction(id10,input).
connectionType(id10,explicit).
port(id12,nil).
location(id12,external).
direction(id12,input).
connectionType(id12,explicit).
port(id14,nil).
location(id14,external).
direction(id14,input).
connectionType(id14,explicit).
port(id2,nil).
location(id2,external).
direction(id2,input).
connectionType(id2,implicit).
port(id4,nil).
location(id4,external).
direction(id4,input).
connectionType(id4,explicit).
port(id57,nil).
location(id57,external).
direction(id57,input).
connectionType(id57,explicit).
port(id58,nil).
location(id58,external).
direction(id58,input).
connectionType(id58,explicit).
port(id59,nil).
location(id59,external).
direction(id59,input).
connectionType(id59,explicit).
port(id60,nil).
location(id60,external).
direction(id60,input).
connectionType(id60,explicit).
port(id8,nil).
location(id8,external).
direction(id8,input).
connectionType(id8,explicit).
port(id92,nil).
location(id92,external).
direction(id92,input).
connectionType(id92,explicit).
port(id95,nil).
location(id95,external).
direction(id95,input).
connectionType(id95,explicit).
port(id17,nil).
location(id17,internal).
direction(id17,input).
connectionType(id17,explicit).
port(id18,nil).
location(id18,internal).
direction(id18,input).
connectionType(id18,explicit).
port(id23,nil).
location(id23,internal).
direction(id23,input).
connectionType(id23,explicit).
port(id24,nil).
location(id24,internal).
direction(id24,input).
connectionType(id24,explicit).
port(id25,nil).
location(id25,internal).
direction(id25,input).
connectionType(id25,explicit).
port(id30,nil).
location(id30,internal).
direction(id30,input).
connectionType(id30,explicit).
port(id31,nil).
location(id31,internal).
direction(id31,input).
connectionType(id31,explicit).
port(id36,nil).
location(id36,internal).
direction(id36,input).
connectionType(id36,explicit).
port(id37,nil).
location(id37,internal).
direction(id37,input).
connectionType(id37,explicit).
port(id38,nil).
location(id38,internal).
direction(id38,input).
connectionType(id38,explicit).
port(id63,nil).
location(id63,internal).
direction(id63,input).
connectionType(id63,explicit).
port(id64,nil).
location(id64,internal).
direction(id64,input).
connectionType(id64,explicit).
port(id65,nil).
location(id65,internal).
direction(id65,input).
connectionType(id65,explicit).
port(id70,nil).
location(id70,internal).
direction(id70,input).
connectionType(id70,explicit).
port(id71,nil).
location(id71,internal).
direction(id71,input).
connectionType(id71,explicit).
port(id72,nil).
location(id72,internal).
direction(id72,input).
connectionType(id72,explicit).
port(id77,nil).
location(id77,internal).
direction(id77,input).
connectionType(id77,explicit).
port(id78,nil).
location(id78,internal).
direction(id78,input).
connectionType(id78,explicit).
port(id79,nil).
location(id79,internal).
direction(id79,input).
connectionType(id79,explicit).
true.

?- 
```
<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
