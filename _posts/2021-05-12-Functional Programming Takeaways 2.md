---
layout: post
title:  "Functional Programming Takeaways 2"
---

## Functional Programming

Functional programming breaks down into two actions:

1. pattern matching
2. text replacement & manipulation

### Pattern Matching

Pattern matching is _parsing_.

Currently, the easiest parsing method is PEG.

My favorite variant of PEG is Ohm-JS.

Ohm-JS claims to simplify PEG parsing, through various complicated means (upper-case vs. lower-case rules).

The real gem in Ohm-JS is the Ohm-editor.

The Ohm-editor simplifies the act of building parsers.

If I were to use some other PEG library, I would use the Ohm-editor first.

### Text Manipulation

Functional programming, and mathematical notation, imposes the restriction that there can be no side-effects.

In fact, this is only a subset of the more important idea of _isolation_.

You can allow mutation, and, you can build components that are arbitrarily complex, _as long as the components are isolated_.

## Isolation
Isolation is more important than complexity.

Isolation is more important than immutability.

### Scalability
Isolation provides scalability.

### Black Boxes
Isolation means that you can treat  Components as black boxes - input & outputs, we can't care about what is inside.
## Everything Is A Fractal

Everything is a fractal.

Everything can be further sub-divided.

That includes everything I say.  Nothing I say is _absolute_, it is _relative_, and, it can be broken down.


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
