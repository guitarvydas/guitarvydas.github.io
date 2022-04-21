---
layout: post
title: "Dependencies"
---
## Dependencies - The Problem of the 2000's
Dependencies in programs are the "global variable" problem of the 2000's.

IMO, the way to think about this problem is:
0. strive for software components that have zero (0) dependencies
1. forget about programming languages and just write software components in a hand-written notation[^diag], that have 0 dependencies
2. look at what you've written and build a programming language that mimics what you wrote in (1).

[^diag]: Better yet, eschew character-based writing and draw diagrams.

## Asynchronous Components

IMO, the solution is to use asynchronous components.

Not components that invoke thread libraries.


Components that are asynchronous from the get-go.

Note that our current notation implies that all programming language statements are *synchronous*.

One must be careful to write pseudo-programs that do not rely on statement sequencing.

### Asynchronous Notation
 Thread libraries treat concurrency as a second class entity, not an integral part of the notation.  
 
 Modeling concurrency in a notation isn't the same as using a notation that is implicitly concurrent.  
 
 For example `f(x,y)->u`[^antilc] implies synchrony, not asynchrony.  There are multiple kinds of synchrony in just that simple statement:
 - `f` is hard-baked into the expression 
 - `CALL / RETURN` implies synchronization of the caller and the callee.  The caller *waits* (blocks) until the callee is finished.
 - `(x,y)` implies that, both, `x` and `y` arrive in a block at the same time (synchronous - time dependency)[^parameters]
 - `->u` implies that all results, packed into `u`, leave in a block at the same time, (actually, the value of `u` depends on the timing of all of its sub-data.  All results need to be generated before the callee deacivates itself and unblocks the caller.
 - worse yet, `->u` uses a different syntax than `(x,y)`.  We describe input parameters as a desctructuring, but describe output parameters (return values) as an amorphous blob.

[^antilc]: I have chosen to not use the most modern form of functional notation to make my points.

Lambda calculus and Currying are inching towards a more-unified syntax.  LC insists that *all* data be created as sequences of functions and that functions be composed (`->`) in a synchronous manner.  LC tends not to describe the destructuring of data items, lumping all data into singular parameters and names (or, nameless stack offsets in the case of De Bruijn notation).  Destructuring can be described as sequences of functions composed in a synchronous manner.  Sequences are but flattened layers of information. Layering, in Lambda Calculus notation, is provided by wrapper functions, which tend to be defined in a flat (non-layered) manner, the layering of which is obfuscated by the notation.

Insisting that *all* data be represented in the same way is a re-discovery of the principles of normalization, espoused in languages like *assembler*.

Insisting that *all* functions be synchronous is a side-effect of using notations that were invented for use with pen-and-paper, instead of using more modern multi-dimensional notations (and processors, like computers).

#### Alleviating Syntax

To alleviate the hard-baked knowledge that `f` is being called, use indirection.  DLLs are an atempt at doing this (an indirection slot is created for each imported function/entity).  C allows this using the `(*f)(...)` notation, but, that notation is too cumbersome.  Even `bash` allows indirection, if you try, e.g. `$f ... ...` instead of `f ... ...`. `Bash` lulls programmers into using a non-hierarchical form of indirection by providing `PATH`, which indirects all function calls to a flat place(s) in the file system.  Worse, `bash` fragments the notation for indirection by providing a bunch of rules that need to be learned by rote memorization.

To avoid the implicit synchrony and blocking of `CALL / RETURN`, 
- don't use `CALL` (or function-calling), use `Send()` to move data to *output* *ports*[^call]
- receive data from *input ports* using 
	- -*handler* functions[^handlers], or, 
	- `Receive()`

[^call]: `CALL` (function calling) should only be used to describe the implementation of *innards* of components, not communcation *between* components.

[^parameters]: Note that compilers implement parameter lists in exactly this manner.  All parameters are evaluated and their values are placed into a block of memory (The Stack), before the callee is activated (unblocked, called).

[^handlers]: ATM, I favour the use of *handler* functions to react to asynchronous inputs.  As I write this, I recognize that this choice produces two different syntaxes - a syntax for input (*handlers*) and a different syntax for output (*Send()*).  Hmm.  Rhetorical question: can *handler* functions be implemented using *Receive()*? Rhetorical question: there is a difference between a theoretical treatment of a concept and a UX for that concept that appeals to non-theorist users.  What is the UX expected by non-theorists, that would be most useful in describing problems of this nature?

To avoid the synchronous tyranny of `(x,y)` parameter list notation, invent a notation that describes layered *ports* of destructurable data, e.g. something like
-`f(a,b)(c,d)(x,y)->...`
	- wherein each block, `(a,b)`, `(c,d)` and `(x,y)` can arrive at different times.
	- this suggestion has bugs, `g` remains hard-wired and direct.  Maybe `f` should be replaced by a reference to an output port, e.g. something like `«p»`, resulting in `«p»(a,b)` and `«p»(c,d)` and `«p»(x,y)`

To avoid anti- "locality of reference" and to favour normalization, use the same syntax for input and output data blocks (ports).
	
## Ports

IMO, software components require explicit ports.

Input ports.

Output ports.

## Call Nothing

IMO, software components cannot "call" other components.

They can only `Send()` messages.

## No Names

Components have their own name-space.

In the name-space, are:
- names of input ports
- names of output ports.

Notably, the name-space does *not* contain the names of other components (including the parent Containers).

A child cannot decide where a message is `Send()`t to.

Only the parent Container can decide how to route messages.

The parent-child relationship is defined at runtime (dynamically).  This allows components to be used in different situations (plugability).

## Flexibility
Components are composed using Container components (recursively - Containers can contain other Containers (or Leaves)).

All message-routing must be done by the Container, not the containee.

The containee can only send messages to its own output ports (not directly to other components).

The Container wires-up and routes messages between containees (children Components).

## Scalability

We know, from human organization principles, that the most scalable organizational structure is a hierarchical tree (not a DAG).

Commands/requests go *down* the tree.

Summaries (data) come back *up* the tree.

No one tree node is overwhelmed with too much data.  A node deals only with summary data.  

Divide and conquer.

## Asynchrony - Fire And Forget

A component that sends a message does not wait for a response by default.

Components are asynchronous by default.

If synchronization is really needed[^eth], you can use messages to perform a synchronization dance (a concept well-explored in networking and electronics).

[^eth]: Note that *ethernet*, which we use on a daily basis, does not use synchronization (it uses a "random back-off" strategy instead of synchronization).

## See Also
[Zero Dependency Software](https://guitarvydas.github.io/2022/04/11/zerodependencysoftwarecomponents.html)

[CALL RETURN Spaghetti](https://guitarvydas.github.io/2020/12/09/CALL-RETURN-Spaghetti.html)

[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)
[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC9EJr0nKHwadbHUtc5zHdmQ/videos)
[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Books](https://leanpub.com/u/paul-tarvydas.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" > 
</script> 