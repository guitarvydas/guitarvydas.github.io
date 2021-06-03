---
layout: post
title:  "Expressiveness"
---
Step back and try to define "expressiveness".

What does that term mean?

Currently, I think that people use the term "expressiveness" to mean Implementation-ability.

Imagine a measuring-stick (aka ruler). It has two tick-marks on it. One is marked "airy fairy" and the other "implementation".

I am trying to point out that there is a third tick-mark in between those two. This one is marked "DI" (Design Intent).

And then, there's a fourth tick-mark, between "DI" and "Implementation". It's marked "Engineering"[^eng].  And then, there are more tick-marks, ad infinitum. Everything is a fractal, we can sub-divide any problem (including sub-divisions).

[^eng]: Engineering is not Coding. Implementation is Coding.

I'm trying to point out that "expressiveness" is a relative term. It is relative to what you want to accomplish.

Currently, Implementation is considered first-class and everything else is considered to be second-class (or lower).

I am trying to point out that Architecture and Engineering (and Testing, and ...) should be considered to be first-class things.

If you accept that "expressiveness" is a relative term, then the idea of _one-language-to-rule-them-all_ evaporates.

You need at least one language for Implementation.

You need at least one language[^lang] for Architecture.

[^lang]: Note that I use the words "language" and "notation" interchangeably. Most people think that languages are big, heavy things.  They, also, think that DSLs are big and heavy. I know that it is possible to cheat and build a _notation_ in an afternoon. Language - to me - doesn't necessarily mean something big and heavy. I'm trying to introduce the term _notation_ to mean a light-weight DSL that takes no more than a few hours to build (maybe as little as a few minutes). I am forced to use the word "language" until the reader(s) knows what I mean when I say _notation_.  When you believe that syntax is cheap, then your workflow undergoes a fundamental change.  Syntax is cheap.

You need at least one language for Engineering.

And so on.

Today, we have many languages for Implementation, and zero languages for just about everything else.

Anecdote: My first full-time job was at Mitel Corp. where I was a "Software Test Engineer". My job was to augment the testing of Mitel's products before they went into the field. Part of my job was to examine designs and to make them more testable. I had the power to request design changes that would improve testability.  Designers would design and I would change the designs.  My goals were very different from their goals.  No one tried to abstract our goals and to union them into some kind of LCD (lowest common denominator).

If you believe, deep down, that _notation_ is cheap, then you can build (and throw away) notations on a whim. I build nontations to help me build notations.

# See Also

[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
