---
layout: post
title:  "Software Components 101 - Part 10 Tweaking the Grammar to Provide More Information"
---
As it stands, the grammar works, but I keep running into trouble with the code outputter (aka code emission).

I've gotten this far, without any real trouble, but, something isn't working.

## The Problem

I want the code outputter to keep track of the object hierarchy and to output containment relations, e.g. `contains(id9,id28)`.

I've roughed-in containment handling, but, it gives wrong answers - sometimes.

## Complexity Tell
The above is a red flag that tells me that I haven't simplified enough.

I can play whack-a-mole and fix edge-cases as they come up, or, I can look for an overriding simplification.

## How Do you Know When To Stop Simplifying?
Everything is a fractal.

Everything can be broken apart and simplified.

How do to you know when to stop simplifying?

You can't know when to stop.

The only rule is: is it good enough to solve the problem-at-hand?

## What is Needed For This Problem

We want to parse something like:
```
a {
  b {
    c
  }
}
```
and we want to output `c` as `a.b.c`.

We need to remember that a contains b, and, that b contains c.

We want to create an ID for each of the objects, a, b, and, c.  

We'll create those IDs dynamically and call the IDs `gobject` (for "graphical object").

We, also, want to track that `container` for each object using a `contains` relationship.

We need:
```
contains(b,c)
contains(a,b)
```
while noticing that _nothing_ contains a.

Actually, the top-level drawing contains a, so we need to make a relation for that?  

Do we want to make an ID for the drawing?.

If we don't create an ID for the drawing, we create an edge-case for the top-level - nothing contains a, but a contains b, and so on.  

The top-level becomes a special case.

Hmm, special cases lead to edge-cases and are a _tell_ of insufficient simplicity.

Maybe that's the answer - every drawing gets an ID and starts the containment hierarchy off.

Later, we're going to want to join drawings to other drawings, but, we haven't started to think about that problem, yet.  Keep things simple.

OTOH, making an ID for the top-level drawing will probably serve us when we need to start solving the problem of how to join drawings together.

Let's do that for now - we can always change our mind.  

If we keep the code simple and concise, changing our minds won't cause many future problems.  

We want to keep the _thinking_ separate from the _coding_.

If we have to re-think a solution that is OK.

If we have to re-code a solution, then we will tend not to allow our re-thinking to change our solution.  

Less code, more thinking.

We should strive to encode _all_ of our thinking into one line of code.  That way, if we change our minds, all we have to do is to change one line of code.

I've never achieved this ideal - only one line of code - but, I've made many designs that have very few lines of "code" (about one page, or about one eye-full).

## Back To The Drawing Board

We are at liberty to change the design completely.

We are always at liberty to make such sweeping changes, but, there things that discourage us from doing so.

Having written too much code discourages us from changing our designs.  

The answer to this problem is simple: write less code.  D'oh.

Spend a disportionately huge amount of time on the design and very little time on creating code.

Throw code away and start again...

### How To Write Less Code?

See my essays entitled "Less Code" and "Writing Code That Writes Code".

Write down the DI (the Architecture), don't spend much time writing down code that has the DI calcified into it.

Simplify the DI until it occupies only one eye-full (e.g. a page, a window).  

No one wants to read your 200-page manual on how to use your DI notation, so keep it simple.  Goals: 1 page for the DI notation manual and 1 page of code in the DI notation[^manual].

[^manual]: Try to fractalize the DI manual.  1 page to get the basics, and a hierarchy of more detailed stuff (fractalized) that might be needed later.  Flat _anything_ is bad.  Flat manuals are TL;DR.

## Tipping Point

I have found that there is a psychological tipping point that affects DI Refactoring[^di].

See my other essay called `DI Refactoring`.


# Red Flag - Whack-A-Mole Tell
Playing whack-a-mole with edge cases is a red flag.

Something is not simple enough.

Ah - the diagrams are diagrams, but we've tangled semantics into the diagrams.

# The End - Begin Again
Let's start again, and make the diagrams simpler.

Plan: 
1. convert the diagrams to markdown.
2. convert the markdown into nested syntax (technical term: CFG)
3. convert the nested syntax into factbases with inferred `contain` facts
4. inference interesting information.

See Part 11, where we start all over again.

[^di]: DI means _Design Intent_.  Often, the term _Software Architecture_ is overloaded to mean DI.


<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
