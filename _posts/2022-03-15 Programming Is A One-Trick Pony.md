---
layout: post
title:  "Programming Is A One-Trick Pony"
---
Programming consists of a single trick[^byrd].

Containment.

We keep re-discovering this trick the hard way.

`(lambda (...) ...)`` is Containment (bound variables).

`{ ... }` is Containment (ASCII Art for "box").

`Structured Programming` is Containment.

`OO` is Containment.

`Divide-and-conquer` is Containment.  Split the problem into 2 problems, Contain each sub-problem.

`Multi-Tasking` is Containment.  A heavy-handed form of Containment.  We can stick any `calculator` into an `envelope` (aka `process`), then, we can yank control away from the calculator at will (`preemption`).

`Computers`, `Laptops`, `Phones` are Containment.  Run many apps, but, contain each of them so that they don't interfere with one another.

`Scanners` are Containment.

The Unix philosopy - `do one job well` - is Containment.

`Pipelines` are Containment.

`MMU`s (Memory Managment Units) are Containment.

`Segmented Memory` is Containment.

`GUIs + JavaScript` are Containment.

`Browsers` are Containment[^distributed].

`Clients` are Containment[^distributed]. 

[^distributed]: Separate computers.

`Spreadsheets` are Containment (cells are containers for formulae and text).

`Variables` are Containment.  Variables contain data in memory cells.  We tend to give names to these containers (although, we are breaking loose of this habit).  Global variables are not-very-well-contained variables.  Programming culture lassoed global variables and tamed them by putting variables into smaller containers (local variables and parameters). Mathematicians have formal names for these concepts (bound and free variables), but, they're really talking about degrees of containment.

Programmers draw boxes within boxes on `whiteboards` to represent programs. Poor containment is immediately obvious.

Using *layers* is Containment.  Each *layer* contains an idea and an implementation of the idea.  The *layers* can be organized hierarchically (or not).

## Hierarchy
In fact, hierarchy is the *second* trick.  Once a program has been chopped up into self-contained units, the units need to arranged in a scalable manner.  

Hierarchy is scalable and forms Containers of Containers.

Humans invented hierarchy and use it daily.  

## Business
For example, successful businesses are arranged hierarchically.  

First, a business is chopped up into smaller Contained units (departments).

Secondly, the units are further contained and rearranged into a hierarchy.

The business hierarchy is drawn out as ORG Charts.

Every department manager reports *upwards* to managers of managers (e.g. VPs).

Managers do not deal with all of the details (in a successful business).  

*Upward* reports elide details.  

*Downward* commands deal only with concepts and not details.

When this hierarchical organization is broken, it is called "micro-management" (downwards) and "going over the boss's head" (upwards).

Business visionaries (e.g. CEOs) sketch out only the overview of a business concept and hire Implementors to fill-in the details, i.e to realize the concept.
- lambda ignores many aspects of computing (e.g. sequencing, history) and implements calculators (in fact, our manifestation of lambda in hardware is that of using a shared global variable (The Stack) and changing it dynamically (CALL/RETURN) and prematurely optimizing it (a stack is a list where the cells have no CDRs (this satisfies the mid-1900s obsession with optimization of memory use))).

[^byrd]: I borrowed this phrase from [Will Byrd's talk](https://www.youtube.com/watch?v=OyfBQmvr2Hc) wherein he states that *lambda* is The Trick.  I disagree with this assessment and think that *lambda* is only a sub-manifestation of The Trick.


## Appendix - Points Not Yet Covered
- [Peter Lee's book](https://www.amazon.ca/Realistic-Compiler-Generation-Peter-Lee/dp/0262121417)
- APIs
- UNIX hierarchy
- middleware
- ignoring details
- mathematics - no layering, flat
- Customer, Architecture, Engineering, Production Engineering, Implementation
- Testing - (1) Test Engineer (2) Testing
- Parsing - grouping phrases into a hierarchy
- OO - grouping objects, but, hierarchical organization is not enforced
- scalability
- PROLOG backtracking - grouping patterns, but, hierarchical organization is not enforced
- The GOAL Of Programming
	- Programming Is Not Notation Worship
	- Notation Worship === "fad"
- Atoms, Molecules
- transit buses are async Containers of async Humans
- Don't Fear The Async
	- riff on Blue Oyster Cult
	- bananas are async
	- apples are async
	- if we cut that banana in half, nothing happens to that apple (it is async (isolated, it has no dependencies on that banana))
- PEG
	- matching nested parens -> containment
- start by drawing a diagram
	- if you can't draw a diagram, then you don't understand the problem (yet)
	- that's OK, at first, since *you don't understand the problem* (by definition - it's a new problem)
		- you will find a plethora of questions that need to be answered before you can draw the diagram
		- getting answers to these questions will aid you in understanding the problem
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
        crossorigin="anonymous" 
        async> 
</script> 
