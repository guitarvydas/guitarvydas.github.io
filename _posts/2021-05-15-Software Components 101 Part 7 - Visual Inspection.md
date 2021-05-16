---
layout: post
title:  "Software Components 101 Part 7 - Visual Inspection"
---
In reviewing the facts in Part 6, I noticed that there is no `contains` relationship.

What is needed: a `contains(ID,shapeID).` fact for every circle and cylinder and rect and comp object.

Further, for sanity checking (aka development testing), we need to add convenience facts `shape(shapeID,"string").`, as we would like to query the factbase to find every `contains` relationship and to find every `shape` of every contained item.

[N.B. Storing the design as a factbase makes it easy to add convenience facts.  We simply add them.  The existing queries will not be affected, since they skip facts that they are not interested in.  In other words, adding extra facts - convenience facts - does not add new dependencies into the factbase.  The existing queries continue to function. Normalizing data into factbase form has given us isolation.]

We simply need to modify the very "top" query to read:

```
  OPML [xmlhdr opmlhdr head body outline endbody endopml] =
    {{ scopeAdd ('counter', 0); scopeAdd ('gobject', "id" + gen ()); }}
    [[${xmlhdr}${opmlhdr}${head}${body}${outline}${endbody}${endopml}]]
```
and we need to push a new ID for every shape:
```
[[${t}${o}\ncontains(${scopeGet ('container')}, ${scopeGet ('gobject')}).\n]]
```

The convenience facts are added by modifying all of the shape rules (circle, cyl, rect, comp, line, arrow), for example:
```
  circleObject [teq dq1 circle spc ubq id ueq dq2] =  [[circle(${scopeGet ("gobject")}, ${id}).\nshape(${scopeGet ('gobject')}, "circle").]]
```
The convenience facts are meant for human-readability.  It turns out that we already have human-readable synonyms.  The addition of `shape` facts is moot (a dead end).  We can leave them in the code, for now, since they do no alter any of the existing queries.

We add a round-trip query and display all parent/child relationships using synonyms.

[In general, I oppose the use of round-trips.  A round-trip is justified, here, because we are bootstrapping and eye-balling results to confirm sanity.  After bootstrapping, round-trips should be unneccessary.  Round-trips are included in post-bootstrap code for one of two reasons:
1. The Notation is not sufficiently powerful.
2. The user(s) do not believe that they can use the notation without resorting to low-level manipulations.
Round-trips are hard to create and cause more work.  The need for round-trips should be a red flag.]

## New Queries
We add the queries:
```
parent(P,C) :-
    contains(PID,CID),
    synonym(PID,P),
    synonym(CID,C).

display(P):-
    setof(C,parent(P,C),Bag),
    format("~w: ~w~n", [P,Bag]).

displayAllPC:-
    setof(P,display(P),_).
```
## Using the New Queries
```
?- consult(fb).
true.

?- consult(q).
true.

?- displayAllPC.
c: [c_a,c_b,c_c,c_d,c_e,c_f,c_g,c_h,c_i,c_j,c_k,c_l]
c_e: [c_e_m,c_e_n]
c_g: [c_g_o,c_g_p,c_g_q]
c_i: [c_i_r,c_i_s]
c_k: [c_h_v,c_k_t,c_k_u]
e: [e_a,e_b,e_c,e_e,e_f,e_g,e_h,e_i,e_j]
e_e: [e_e_k,e_e_l,e_e_m]
e_g: [e_g_n,e_g_o,e_g_p]
e_i: [e_i_q,e_i_r,e_i_s]
z: [a,b,c,d,e,f,g]
true.

?- 
```
## Error - Missing Node
Looking a the "e:" line, we see that e_d is missing.

This is probably human error.

Let's look at the `diagrams.opml` file.

Indeed, a node was missing.

We add:
```
				<outline text="circle “e/d”">
					<outline text="color=yellow" />
				</outline>
```
and, now the result looks correct (that doesn't mean that it _is_ correct, but only that it passes visual inspection)
```
?- consult(fb).
true.

?- consult(q).
true.

?- displayAllPC.
c: [c_a,c_b,c_c,c_d,c_e,c_f,c_g,c_h,c_i,c_j,c_k,c_l]
c_e: [c_e_m,c_e_n]
c_g: [c_g_o,c_g_p,c_g_q]
c_i: [c_i_r,c_i_s]
c_k: [c_h_v,c_k_t,c_k_u]
e: [e_a,e_b,e_c,e_d,e_e,e_f,e_g,e_h,e_i,e_j]
e_e: [e_e_k,e_e_l,e_e_m]
e_g: [e_g_n,e_g_o,e_g_p]
e_i: [e_i_q,e_i_r,e_i_s]
z: [a,b,c,d,e,f,g]
true.
```
<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
