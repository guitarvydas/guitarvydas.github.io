---
layout: post
title:  "Word® vs. Mathematics"
---
## Immutability and Mathematical Notation

Mathematical notation relies on immutability.

If you have immutability, you can replace patterns with impunity.

Note that I'm not describing *all* of mathematics, just the notation part[^1].

[^1]: At a simplistic level, mathematics is composed of 2 portions (1) Notation, and, (2) Thinking.

## Search and Replace

The *notation* part of mathematics boils down to a simple set of principles
1. find a pattern
2. replace the pattern
3. repeat.

### Word

Word® does *search and replace*.

Can Word® do mathematical manipulation for us?

## Recursive Search and Replace

It is easier if your searcher-and-replacer works recursively.

REGEX is flat (non-recursive).

Parsers are recursive.

### PEG vs REGEX

PEG[^1] does recursive parsing and is "better" than REGEX in that regard.

[^1]: Ohm-JS is currently my favourite form of PEG.

## UNIX Immutability

Immutability is, actually, *isolation*.

You can re-arrange things if you can guarantee that this doesn't cause unintended side-effects.

UNIX® providex *isolation*.  With C, yet.

UNIX® commands are completely stand-alone.  If you change the source for `cat.c`, the operation of `sed.c` doesn't change.

UNIX® creates *isolation* at runtime by piping (isolated) commands together.

### What's Inside?

Who cares what's inside? 

Do we care if a UNIX® command is written in C or in Haskell?  

No. 

We only care that the commands are isolated from each other. We can make the internals of the commands better, later.

Achieving isolation - immutability - at compile-time is just icing-on-the-cake (aka optimization).

# See Also

[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
