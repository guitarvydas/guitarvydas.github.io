---
layout: post
title:  "Compiling Diagrams To Code"
---

My inspiration for using components came from Harel’s Statecharts paper (plus the immediate need to control a 4-headed 68000).


I wrote a textual statemachine compiler for that project.

After that, I discovered that Harel’s Statecharts were really 2 technologies:
1. HSM - hierarchical state machines (no concurrency, no orthogonal states).
2. concurrent components.

I kept cycling on that idea and figured out how to compile diagrams to code.

Using PEG and PROLOG, it is easy to compile diagrams[^furtherReading].

[^furtherReading]: For more on this subject, search my blog for keywords such as _factbases_ and _triples_.

Diagrams make the most sense when the boxes depict concurrent software components.

Using synchronous languages for diagrams tends to fail.

My diagrams are based on the EE paradigm.

I think in terms of discrete events and communicating state machines,

One needs the equivalent of structured programming for message-passing.  

That’s something that is missing from the Actor model.

Enabling a paradigm is not the same as encouraging the use of a paradigm[^asm].

[^asm]: If it were good enough to simply enable a paradigm, then we'd be coding everything, OOP and FP, in assembler.  The paradigm needs to be encouraged (enforced), like what Smalltalk did for OOP.

Trees scale.

Graphs (which imply inter-dependencies) do not scale well.

We used to build POS embedded applications with some 300 components on 8-bit CPUs with very little memory (12K and up) (for IVI, since bought up by Ingenico).

Obviously, a system of 300+ components must be structured in some kind of hierarchy, to be understandable.

Again, having concurrent nodes in the hierarchy makes things more manageable. Current GPLs encourage anti-concurrent design[^threadLibraries].

[^threadLibraries]: Any language that uses a thread library treats concurrency as an after-thoughts and a second-class entity.

# See Also

[Communicating State Machines](https://guitarvydas.github.io/2021/08/16/Communicating-State-Machines.html)
[Triples](https://guitarvydas.github.io/2021/03/16/Triples.html)
[Factbases 101](https://guitarvydas.github.io/2021/04/26/Factbases-101.html)

[PROLOG For Programmers](https://www.youtube.com/watch?v=QOYAHoLiyg0)

[Blog](https://guitarvydas.github.io)

[Videos](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy50fIg)

[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
