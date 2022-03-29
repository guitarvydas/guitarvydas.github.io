 ---
layout: post
title:  "Dependencies"
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

No one tree node is overwhelmed with too much data.  A node deals only with summary data.  Divide and conquer.

## Asynchrony - Fire And Forget

A component that sends a message does not wait for a response by default.

Components are asynchronous by default.

If synchronization is really needed, you can use messages to perform a synchronization dance (a concept well-explored in networking and electronics).

## See Also

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