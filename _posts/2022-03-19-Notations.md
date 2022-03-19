---
layout: post
title:  "Notations"
---
The [BLC Blog](https://justine.lol/lambda/) contains this statement:
```
...
Unlike LISP, lambda calculus does head reduction, 
...
```

Splitting hairs, LC is a *notation* that *uses* Lisp like an *assembler*.
```
λ0
```
becomes
```
(callFunctionWithOneArg (lambda (x) x) (lookupInEnvironment 0))
```
(where "x" is any name),
or
```
callFuntionWithOneArg (a, b)
```
where `a` is
``` 
function (x) { return x; }
```
and `b` is
```
lookupInEnvironement(0);
```

A *notation* elides certain repetitive operations.  Clearly, the LC notation is shorter than the Lisp-y notation, which leads to insights about how functions can be plumbed together.  Yet, LC *notation* is less "powerful" than Lisp-y notation, since certain things are impossible in LC while possible[^possible] in Lisp-y notation.

[^possible]: For example, Common Lisp allows mutation while LC disallows mutation. Does this mean that mutation is good or does it mean that mutation is bad? It depends.

Bizarrely, "power" implies closer-to-assembler-ness.

When we take McCarthy's original FP *notation* and hack mutation and looping into it, we get a "more powerful" assembler, called Common Lisp.

Elision, in some beholders' eyes, looks like obfuscation. People hate mathematics because it elides (aka obfuscates) certain concepts. Mathematicians love mathematical notation. That would be good enough as long as we're not forced to use mathematicians' favorite notation for *everything*.

For example, for certain problems, spreadsheet notation is perceived as being "better" than mathematical notation. If you want to understand the gory details of something, you use mathematical notation, if you want to understand income statements and balance sheets, you use spreadsheet notation.

Hacking on mathematical notation, e.g. to insert the concept of time/history, makes that notation "closer to assembler", but, doesn't help in visualizing what is going on.  Feynman used diagrams and elided Greek symbols to gain a better understanding of a certain aspect of Physics.

Choosing an appropriate notation depends on the problem that you are trying to solve.

Choosing a notation before understanding the problem is a *fad*.

## Switching Notations
Actually, you can choose a notation to *start* thinking about something, but, you have to remain open to the idea of switching notations or of inventing better notations.  

How do you know when to switch notations?  

I don't know, but, it probably has something to do with understanding (boxing, scoping) the limits of a notation.  

You look for *tells*.

A *tell* would be when you need to resort to clever twists of the notation.

An example: J. Tunney's Sector Lisp is an example of really pure Functional Programming.  No mutation allowed - GC becomes easy and small. [*Mutation hacked into Functional Programming led to random access heaps which led to more-and-more-elaborate garbage collectors and cleverness.*]

Tunney's BLC is even smaller than Sector Lisp.  What can we learn about the limits of Lambda Calculus notation from that?


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
