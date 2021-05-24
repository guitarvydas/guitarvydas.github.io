---
layout: post
title:  "UNIX Takeaways"
---

- Isolation
- Coordination Language
- Concurrency

# Threads are Isolation

Programs are completely separated from each other and can communicate only over very restricted channels.

Threads are _envelopes_ that one can drop _calculators_ into.

# Coordination Language

PLs have traditionally been restricted to expressing the contstruction of synchronous calculators.

Few PLs address the issues of distributed programming[^alib].

/bin/sh ("&" and "|") is a DSL for creating higher-level concurrent abstractions.

## PID

PIDs - process ID - are handles to first-class components.

[^alib]: Distributed programming is, currently, only addressed by second-class, assembler-like operations and libraries.

# Concurrency

Concurrency is a programming paradigm.

Parallelism is an application problem that needs to use the concurrent paradigm

# Anti-Takeaways
## Time-Sharing
## Memory Sharing
## Closures
	Threads are just closure-wannabees.  (Maybe I mean /CCs?).
	UNIX threads are just ad-hoc implementations of closures in C.
## Dependency Spaghetti
## Rendezvous
Attempt to corral concurrency by making _everything_ synchronous.
## Syntax for Distributed Programming is Minimal
The UNIX shell syntax for distributed programming is muddied by the inclusion of many other features[^soc].
[^soc]: Lack of Separation of Concerns
## Continued Conflation and Muddied Waters Between Programming and O/Ss
UNIX contains several fundamental advances in PL features (e.g. |, &, fork, etc).

These PL advances have, unfortunately, been conflated with Operating Systems and have largely been ignored in PL designs.
## /bin/*sh Union of Coordination and String Processing and ...
  O/Ss are just libraries.
  
  Windows, MacOS, Linux are just applications[^os].
  
  Not every app should have all of the above principles built-in, e.g. not every app needs memory sharing and time-sharing.
# Pipelines vs. Isolation
UNIX popularize pipelines of isolated components.

These advances have been, unfortunately, overlooked due to 
- conflation with heavy technologies (e.g. O/Ss)
- premature optimization (e.g. the ideas of _isolation_ were burned into hardware before they were sufficiently explored, e.g. C had some useful ideas about _isolation_ but these were missed in lieue of C's system-language features)
# See Also
Concurrency is not Parallelism - Rob Pike

https://guitarvydas.github.io/2021/01/14/References.html
https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html
  
<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
