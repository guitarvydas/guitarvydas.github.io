---
layout: post
title:  "Software Components 101 - Part 9 - What's Next?"
---

So, what kinds of queries do we need to build next?

Let's recap our goal:
- we want convert our diagram to code.

RQ: [Rhetorical questions][^pattison]
- What have we got?
- What do we need?

We have:
- Basic queries
- We know what things are components
- We know what things are ports 
- We know stuff about the ports - external/internal, input/output, implicit/explicit
- We know which things are arrows and which way they point (aBegin and aEnd).

So, what else do we need to know to satisfy our goal?

For one, we need to know which components are _foreign_, i.e. not implemented in DASL as composite components.

What are the queries that will give us that information?

First guess - any component that does not contain other components is _foreign_.  

Is that good enough?

We don't need to answer that question at the moment - that would be over-confident, Waterfall-style thinking.

Let's build a query based on the above and see where that gets us...

We can test our ideas, since the drawings are small enough to eye-ball.  Gross bugs in the design will jump out at us.

For starters, let's see what we should expect.

I count 7 missing components - aka _foreign_ components.

1. [make instance]
2. [invent name]
3. [recursively instantiate]
4. [insert child into children of my runnable]
5. [clone connection]
6. [fixup connection]
7. [insert connection into runnable].

Let's see if our query returns those 7 - and _only_ those 7...

[Aside: The missing components should be drop-dead simple to implement.  Are they?  If not, maybe they need to be decomposed even further.  Goal: implement each component using 1 line of JavaScript[^3].  Keep this goal in mind as we proceed.]

[^3]: If we can write these in JS, then we can write them in _anything_ :-).

[^pattison]Pat Pattison teaches songwriting and poetry.  He often says (paraphrased) "What have you got? What is different?".

## Debugging Using Queries
Hmm, something isn't working.

Let's take one example of a missing (foreign) component and follow it through the queries.

Let's pick on [clone connection].

It's human-readable synonym is e_e (from the diagrams, tab "Rough-in Processes Labelled").

What is its machine-readable ID?
```
?- synonym(ID,e_e).
ID = id61 ;
false.

?- 
```
It's "id61".

Sanity check - is id61 a Composite Component?
```
?- compositeComponent(id61).
true ;
true ;
true.

?- 
```
Woah, that doesn't seem right.  How did that answer come into being?

We examine the definition for `compositeComponent`.

We see that checking for `contains` is not enough.

A component can contain things other than components, such as Ports.

What we want is to check if a composite component contains another component.

We extend the query to succeed only if the contained item is another component:
```
compositeComponent(C):-
    comp(C,_),
    contains(C,Sub),
    comp(Sub,_).
```

And try again:
```
?- consult(fb).
true.

?- consult(q).
true.

?- compositeComponent(id61).
false.

?- 
```
That's better.

Now, let's add a query for missing components
```
allCompositeComponents(Cs):-
    setof(C,compositeComponent(C),Cs).
missingComponent(C):-
    comp(C,_),
    allCompositeComponents(Composites),
    \+ member(C,Composites).
```
and check its result:
```
?- consult(fb).
true.

?- consult(q).
true.

?- missingComponent(C).
C = id15 ;
C = id21 ;
C = id28 ;
C = id34 ;
C = id61 ;
C = id68 ;
C = id75.

?- 
```
That's more promising.  The query says that 7 components are missing.

We are in the middle of development.  Anything could be wrong.  Errors could be due to logic problems, or, simply due to typos.  Typos result in "random" behaviour.  Sometimes you can deduce where a random behaviour is coming from and sometimes you can't.

Let's sanity check those 7 missing components.
We can write the query at the REPL, or put it in a file.  It is simple enough to enter at the REPL.

```
?- missingComponent(C),synonym(C,Syn).
C = id15,
Syn = c_e ;
C = id21,
Syn = c_g ;
C = id28,
Syn = c_i ;
C = id34,
Syn = c_k ;
C = id61,
Syn = e_e ;
C = id68,
Syn = e_g ;
C = id75,
Syn = e_i ;
false.

?- 
```
It says that the missing components are:
- c_e
- c_g
- c_i
- c_k
- e_e
- e_g
- e_i.

Looking at the diagram, we see that those synonyms match up with the components that we expect to be foreign (aka missing).

Let's rewrite this query as:
```
describeForeignComponent(C):-
    missingComponent(C),
    synonym(C,Syn),
    format("foreign: ~w~n", [Syn]).
describeForeignComponents:-
    setof(C,describeForeignComponent(C),_).
```
and try
```
?- consult(fb).
true.

?- consult(q).
true.

?- describeForeignComponents.
foreign: c_e
foreign: c_g
foreign: c_i
foreign: c_k
foreign: e_e
foreign: e_g
foreign: e_i
true.

?- 
```

What else is needed?

A connection list for every composite.

## Arrow Bug
Writing a query for connection lists starts by finding all arrows directly contained by a component
```
?- consult(fb).
true.

?- consult(q).
true.

?- arrow(C,A),comp(C,Syn).
false.

?- 
```
Bug: arrows don't seem to be connected to their containers.  

We added a "container" symbol earlier.  

We should be using it for arrows.
```
  arrowObject [teq dq1 comp spc idsender @ws idsreceiver dq2] =
  {{ scopeAdd ("arrow", "a" + gen ()) }}
  [[
arrow(${scopeGet ("container")}, ${scopeGet ("arrow")}).
arrowBegin(${scopeGet ("arrow")}, ${abegin (idsender)}).
arrowEnd(${scopeGet ("arrow")}, ${aend (idsreceiver)}).
shape(${scopeGet ('gobject')}, "arrow").]]

```

Now, all arrows look like they are contained by only the top.

## Bug
Visual inspection of the results indicates that something is wrong.

It turns out that the .opml file contains a typo `c/h/v` instead of `c/k/v`.

```
					<outline text="rect “c/h/v”">
						<outline text="color=yellow" />
					</outline>
```

Changing this line (and bringing `Diagrams 1 2 1.cod` up to date) results in:
```
?- consult(fb).
true.

?- consult(q).
true.

?- describeArrows.
id55: [[e_c,[e_e_k]],[e_b,[e_e_l,e_g_o]],[e_e_m,[e_f]],[e_f,[e_g_n]],[e_g_p,[e_h]],[e_h,[e_i_q]],[e_a,[e_i_r]],[e_i_s,[e_j]],[e_j,[e_d]]]
id6: [[c_c,[c_e_m]],[c_e_n,[c_f]],[c_f,[c_g_o]],[c_b,[c_g_p]],[c_g_q,[c_h]],[c_h,[c_i_r]],[c_i_s,[c_j]],[c_j,[c_k_t]],[c_a,[c_k_u]],[c_k_v,[c_l]],[c_l,[c_d]]]
true.

?- 
```
Which looks OK.

## Completing the Diagrams

What is still missing?

`Diagrams.opml` contains only the two components "c" and "e".

We will finish the full set of diagrams in Part 10.


<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
