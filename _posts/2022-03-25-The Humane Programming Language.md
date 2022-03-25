---
layout: post
title:  "The Humane Programming Language"
---
## Spectrum of Languages
Broadly, there are two extremes in programming language design:
1. end-user-oriented - "humane" from the end-users' perspective, but, theoretically unsound
2. theoretically-oriented - self-consistent, but "inhumane" from the end-users' perspective

What is the middle ground?

We need a version of [The Humane Interface](https://en.wikipedia.org/wiki/The_Humane_Interface) for programming language design.

## Programming Languages Are IDEs

The goal of programming is to control the operation of a machine.

Programming languages are simply IDEs for programming machines.

## λ Calculus

A concrete example of (2) - theoretically sound, but, inhumane, programming language is the λ Calculus.

The following is *reverse* in λ Calculus[^jtar] :
```
λa.a(ω(λbcde.d(bb)(λf.fce)))⊥
```
(This becomes even harder to read when De Bruijn indexing is used).

[^jtar]: From [BLC](https://justine.lol/lambda/)

Clearly, one wouldn't expect spreadsheet users to use λ Calculus instead of the high-school math functions that they are used to.

## Question

So, what is the "science" behind wrapping theoretically-sound operations in sugar-coated syntax that makes for a "good" programming language?

### Problem Space

Firstly, it depends on the problem space.  Spreadsheet users want "simple to use" functions.  They don't want to see the power of λ Calculus or the power of Python.

### One Language To Rule Them All - NOT
I argue that there can be no *one* programming language that will satisfy everone.  

*General purpose programming languages* are dead to me.

### Implications

The implication is that we need tools to help us build lots of programming languages, and, we need tricks to make the act of building languages proceed more quickly.

#### PEG

PEG[^peg] - Ohm-JS - is a step in that direction.

[^peg]: Parsing Expression Grammars.

#### Humane Interface For Programming Languages

We need to explore / characterize what end-users *think* is simple.

#### Simplicity, Complexity

Simplicity is defined as "lack of nuance".

How can we hide/elide nuance without removing nuance?

#### Layers

We need to employ layered design.

Layers are infinitely recursive.  

It is not good enough to think in terms of only two (2) layers
- high-level vs. low-level  
- compile-time vs. runtime.

## Syntax
End-users often use diagrams - e.g. whiteboards and paper.

Our programming languages are relegated to being text-only[^text].



[^text]: The reason for this is historical.  In the mid-1900s, it was very expensive to make hardware that operated on anything but non-overlapping, grids of small bitmaps (aka characters).

### Containment

People think in terms of containers - dolls nested within dolls.

Containment is easy to express on diagrams.

Containment is less-easy to express in text.  We have spent decades crawling out of the hole created by our use of text-only languages (Structured Programming, Global-vs-scoped variables, OO, λ Calculus, namespaces, etc., etc.).

#### Containment Diagram

![Containment](/assets/containment.png)

#### Containment Text
```
{
  var x;
}
```
Note that if `var x` appears outside of the braces, the variable `x` is no longer contained.

It happens so often that we've given this condition a special name - *global variable*.

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
        crossorigin="anonymous" > 
</script> 