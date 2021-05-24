---
layout: post
title:  "Multitasking Takeaways"
---
# Multitasking
## The Bad Parts
- time-sharing
- memory-sharing

## How To Avoid Time-Sharing
Use multiple CPUs.  

(e.g. rPIs are cheap.  Laptops are fairly cheap.  Smart Phones are cheap (everybody has one)).

## How To Avoid Memory-Sharing
Use Send().  

_Only_
	
### Immutability
Immutability is but one way to avoid memory-sharing.
### Ownership
Ownership is but one way to avoid memory-sharing.
## Isolation
Isolation is a superset of ownership and non-mutability.

Ownership and non-mutability are but implementation details (towards achieving isolation).

### Deja Vu
Have we already tried _isolation_?

Yes - for example UNIX pipelines provide _isolation_.

Yes - distributed processing involves _isolation_.

Yes - HTML + Javascript provides distributed processing.

### Encapsulation
OO-style encapsulation encapsulates data.

Q: Does OO encapsulate control-flow?

Q: Does OO encapsulate control-flow? Consider method over-riding.

### GOTO
GOTO modifies control flow.

Q: Can you read programs written in GOTO style?

### CPS
CPS (Continuation Passing Style) encapsulates control flow and data.

Q: How does CPS compare to GOTO?

Q: Can you read programs written in CPS style?

### Spaghetti, Complexity, etc., etc.
If a component is _isolated_, then, we don't care - can't care - if it uses mutable state, or, is complex, or, is coded in a non-structured manner.

### ICs - Integrated Circuits
Electronics ICs are built using oxides (rust).

We run software on top of various oxides.

When we pull out a 7400 chip out of a circuit and replace it with a 7400 from another manufacturer, do we care what variation of oxide the other manufacturer used?

### Homebrew NMOS Transistor Step by Step - So Easy Even Jeri Can Do It

[Homebrew NMOS](https://www.youtube.com/watch?v=w_znRopGtbE)

Q: Does Jeri's NMOS transistor use immutable state?  

Q: Does Jeri's NMOS transitor use ownership?  

Q: Do you care?

Q: Do your answers change if Jeri were to build a CPU instead of single transistor?
## Referential Transparency
Referential Transparency refers to the idea that one Component can replace another Component.

Q: What is the base minimum required for Referential Transparency?  Pick only one, the most important one:
- Immutable State  
- Ownership  
- Isolation

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
