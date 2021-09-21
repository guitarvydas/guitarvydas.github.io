---
layout: post
title:  "Asynchronous Thinking"
---

# Introduction

Functions cannot describe what happens when a component consumes input but produces no output. There is no f(x) for this situation.

Async thinking has no problem with this concept. 

In an async solution, one might use "consume-but-produce-nothing Components" - but, that kind of solution is not expressible in functional (synchronous) thinking

It's "magic". 

If you use f(x) notation, you end up not being able to even _think_ about this kind of solution. 

It's akin to having Natural Numbers with no 0 - you think that you can talk about numbers, but certain kinds of things just can't be expressed.

Corollary: Asking programmers to specify Async Components and FBP workflow is asking them for Rube Goldberg ideas derived from synchronous-only thinking.

# Discussion

Programming asynchronously is _VASTLY_ different from sequential programming, yet, the words used to explain both are frighteningly similar.  This means that it is virtually impossible to explain how to use asynchronocity using only words (I've been trying, I'm up to 330+ blog posts, but have yet to find the sweet spot).

Henry Ford is attributed with saying "If I had asked people what they wanted, they would have said faster horses".

The first use of electric motors was to power textile mills, by pumping water uphill to make artificial streams that ran the water-wheels that ran the textile mills.

At first, it was thought that computers were only good for building ballistics calculators.

I would suggest that, instead of the question "what components do you want?" and "what workflow do you want?", the question becomes "what applications are wildly popular?". Then, re-implement one such application using asynchronous methods.

"Give a man a fish, he eats for a day. Teach a man to fish, he eats for a lifetime."

# CALL/RETURN

To emphasize the vast chasm in belief structures, imagine CALL/RETURN.

CALL/RETURN restricts the programming domain in several ways:
1. CALL/RETURN performs scheduling (the caller is suspended, the callee runs immediately).
2. Parameters are delivered in a synchronous block - all at the same time.
3. Return Value(s) are delivered in a synchronous block - all at the same time.
4. The Callee springs to life then dies.
5. We (the Royal We) add a kludge, called "Exceptions" to the syntax of CALL/RETURN to compensate for the shortcomings of the kludge that we call CALL/RETURN.
6. CALL/RETURN is implemented - cast in hardware - using a global variable.

We (the Royal We) use an artificial kludge to take control back in situation #1. Operating systems like to think that they control scheduling, but CALL/RETURN violates that notion. Operating systems use "preemption" to wrench scheduling control away from the caller. Preemption comes with its own baggage cart of accidental complexity.

Asynch Components drive a stake through the heart of CALL/RETURN. Once you know how to program asynchronously, you can't unknow how. Until you know this, though, you are only looking at shadows on the wall (often called "thread libraries", "lazy evaluation", etc.) and you couch *everything* in the language of not-knowing.

Note that Relational Programming and FP are - slowly - learning how to expunge CALL/RETURN from notations.

Note that internet programming and distributed programming (e.g. blockchain, p2p) are - slowly - exposing the fallacy of CALL/RETURN.

Thinking-in-async is very, very, very different from thinking-in-sync.  Async solutions are very, very, very different from sync solutions for the _exact same_ problem.

# Attributions

I would like to thank Ken Khan for pointing out the "horses" statement to me.

The story about the first use of electric motors comes from Tom Goodwin's book "Digital Darwinism".

# See Also

[CALL/RETURN Spaghetti](https://guitarvydas.github.io/2020/12/09/CALL-RETURN-Spaghetti.html)
[blog](https://guitarvydas.github.io)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
