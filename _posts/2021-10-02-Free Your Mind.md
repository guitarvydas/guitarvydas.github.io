---
layout: post
title:  "Free Your Mind"
---

# Elephant in the Room

Computers are asynchronous.

Period.

# Async vs. Sync

Trying to program computers using synchronous methods is a tactic.

Over-using the synchronous tactic will cause accidental complexity, for example callback-hell, etc.

# Step 1 Before Step2

Most people (non-programmers) already understand asynchronous processes.

For example, *cooking recipes* are often arranged in an asynchronous manner:

1. Boil the potatoes. 
2. 2 While the potatoes are boiling, chop up ..."

Five (5) year-old children are taught hard realtime notations

- piano lessons
- music scores.

CEOs understand asynchrony inherently and use *whiteboards* to communicate their intentions.

# Control-Flow

Asynchrony is about control-flow.

Control-flow cannot be expressed as OO.

Control-flow cannot be expressed as FP.

Control-flow cannot be expressed as rendezvous multi-tasking (Rendezvous is another express-async-as-sync tactic).

[*Actually, the above is not strictly true - it is possible to express control-flow in these paradigms, but it isn't as easy as it would be in control-flow-based paradigms.*]

[This leads into the notion of decoupling syntaxes - one syntax for data structuring, another syntax for control-flow structuring.]

# How to Express Async?

## Statecharts

[Statecharts Presentation  (Papers We Love)](https://guitarvydas.github.io/2020/12/09/StateCharts.html)

[Harel's Original Paper](https://www.inf.ed.ac.uk/teaching/courses/seoc/2005_2006/resources/statecharts.pdf)

[Statecharts Again](https://guitarvydas.github.io/2021/02/25/statecharts-(again).html)

## Drakon

[Drakon Editor](http://drakon-editor.sourceforge.net)

## FBP

[Flow Based Programming](https://jpaulm.github.io/fbp/)

## ASCs - Asynchronous Software Components

(see my [Blog](https://guitarvydas.github.io/2021/09/21/Table-of-Contents-Sept-17-2021.html), search for "Isolation", Software Components", "Software Components 101", "ASC", "DaS", etc., etc.)

## Diagrams (DaS)

Diagrams of asynchronous components form a control-flow-based paradigm.

Diagrams built using the synchronous paradigm tend to fail - they are harder to build and less meaningful.

# See Also

[Blog](https://guitarvydas.github.io)
[Table of Contents](https://guitarvydas.github.io/2021/09/21/Table-of-Contents-Sept-17-2021.html)
[Videos](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy5)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
