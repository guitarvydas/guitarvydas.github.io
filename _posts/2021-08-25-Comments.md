---
layout: post
title:  "Comments"
---
I recently finished the language jam.

The theme was "first class comments".

This immediately brings up the question `what are comments used for?`

I see 3 use-cases, at the moment:
1. Explain the Code.
2. Explain the Architecture.
3. Pragmas.

In my opinion, #1 is redundant - the code already explains what the code is supposed to do.

#3 is already handled by compilers in various ways.

That leaves #2 - Explaining the Architecture.

How do you explain the Architecture in a first-class way?

I think that explaining-the-Architecture is a language unto itself.

The goals of an Implementation Language - like Haskell, Python, etc. - are quite different from the goals of a language targeted at explaining Architecture.

Furthermore, I think that _diagrams_ are a simple step towards explaining Architecture. 

Data-point in support of that last sentence - just about everyone who isn't interested in the details of an implementation, sketches the Architecture on a whiteboard or on a napkin.

FYI, I call this DI - Design Intent.

So, what does it mean to have a way to express DI in a first-class manner?

To me, this means:
1. Draw sensible[^sensible] diagrams.
2. Compile the diagrams to executable code.

[^sensible]: What is a sensible diagram? Some agreed-upon convention(s) for diagramming. Something that is not ad-hoc. Something that is layered and not dripping with details (at any one layer).

So, that is what I tried to do in 48 hours in my entry in the langjam.

I created 2 diagram conventions (one for expressing sequencing DI and one for expressing details).

I created compilers for the diagrams (starting with .drawio diagrams, using Ohm-JS, PROLOG and my JS-emitting `glue` tool).

To keep things simple-enough to be working in 48 hours, I emitted `bash` code. 

Actually, there was an ulterior motive to using bash. I know, from experience, that to build sensible diagrams, you need to start with the idea that everything-is-concurrent-by-default. Bash (and /bin/sh, etc.) is an easy way to get default concurrency (but not without warts, since bash insists on creating rendezvous-style concurrency, which is least helpful for everything-is-concurrent-by-default thinking).

I got it working and posted in time.

Everything is "simple" (simple means "lack of nuance").  There are some 6+ passes of Ohm-JS, but each is very simplistic. There is some PROLOG, but it is used mostly for querying and exhaustive search, all of which could be done in a more bug-ridden form as nested loops in any other language.  There is some JS, but, I generated most of it using my `glue` tool. And there is a factbase (triples) which fits neatly onto JSON and onto PROLOG.

Post-jam: I'm currently working on an eat-your-own-dogfood version of the diagrams.

# Github

[my code](https://github.com/guitarvydas/jam0001/tree/main/guitarvydas)

[langjam github and voting](https://github.com/langjam/jam0001/issues/280)

# See Also

[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy5)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
