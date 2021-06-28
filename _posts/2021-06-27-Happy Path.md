---
layout: post
title:  "Happy Path (Part 1)"
---
# Happy Path
A _happy path_ is defined as the control flow followed by a program to handle the backbone of an application.

The assumption is that there is only _one_ backbone for an application, and other paths are exceptions, by definition.

The assumption is that the _Happy Path_ is a first-class construct, while the rest of the paths are second-class constructs.

I disagree with the above assumption.

I believe that a program must handle _all_ paths through an application and that _all_ paths are first-class constructs.

With the rise of distributed programming[^distributed], it is important to consider _all_ paths.

[^distributed:] For example, blockchain, p2p, internet, and HTML.

I think that Dave Ackley's[^ackley] MFM and Robust Computing work also denies the existence of only a single path, although he may describe the problem differently.

[^ackley:] https://www.cs.unm.edu/~ackley/

I believe that most PLs (Programming Languages) emphasize the single-path perspective and relegate all other paths to a lesser status[^secondclass].

[^secondclass:] For example, JavaScript callbacks, and thread libraries.

I believe that notation influences thinking, and, therefore, we must begin using PLs that treat _all_ programming paths as first-class constructs.

## Wikipedia
The Wikipedia entry for "Happy Path" perpetuates this unfortunate perspective:

"... is a default scenario featuring no exceptional or error conditions. ..."

[^wiki:] https://en.wikipedia.org/wiki/Happy_path

## PLs Focus on The Happy Path

## Every Other Path Must Be Sad

(tbd)

## Abdication of Error Handling

## Elm
## Functional Programming Model
Functions are one-in-one-out constructs, everything else is an exception.

# Drakon

http://drakon-editor.sourceforge.net

# Railway Oriented Programming

https://vimeo.com/113707214

# Diagrams
Diagrams allow expression of multiple outcomes while retaining the essence of mathematical manipulation (aka copy/paste).

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
