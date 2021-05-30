---
layout: post
title:  "RY - Repeat Yourself - As a PL Primitive"
---

# RY vs. DRY

DRY means "Don't Repeat Yourself".

Programmers learn to manually perform DRY.

Most people, though, find RY - Repeat Yourself - to be the first programming idiom that they use.

Grab a piece of working code, then hack on it.

Later, RY brings trouble.  Programs built using RY tend to become large and unwieldy.  

RY programs are hard to maintain.  

One bug-fix might affect a piece of code that has been copy/pasted in a number of places.  Each copied piece must be repaired.

Programmers use _libraries_ to manually manage DRY.  Instead of copying pieces of code, the code is moved to a library.  Programs reference the library (instead of cut/pasting the code).

PLs are designed to enable manual DRY.  Code that is (manually) moved to a library is replaced by a single-line reference to the library (a CALL).

# IDEs for RY
IDEs could be designed to support automation of DRY.

Currently, we use CUT/PASTE edit operations to implement RY (and, later, DRY).

Instead, we could use some other gesture to copy/paste likenesses of code.

Our IDEs+PLs could support `like` operators, meaning "this code is like that code over there".

The shared code might appear in gray font, with some transparency.

If one hacks on the code, the new changes appear in a solid colour and no transparency.

The system (IDE + PL) remembers what the original code is and what the changes (diffs) to it are. The programmer sees the code in whole and doesn't need to remember to move it to a library.

`Github` and `diff` already do something like this, except backwards.  Programmers started out using under-powered hardware and developed manual ways of doing things that could be automated today.

# Paul Bennett "Framing Software Reuse"

Paul Bennett discusses _multiple use_ of code, as opposed to simple _reuse_.

# Chanchal Roy, Cordy "NiCAD"

Roy proposes a system for clone detection.

If we had IDEs+PLs that allowed us to say that a piece of code is _like_ another piece of code, we would not need to detect clones (we would simply tell the system about the clones we intend to build).

# Word Processors

In word processors, such as Microsoft Word, select/control-C/control-V means COPY/PASTE.

This keyboard/mouse gesture could be repurposed to mean COPY-LIKENESS and remember (using diff) where the code came from.

# Collaborative Editing

Many online word processors support collaborative editing and change management.  

This same set of techniques could be applied to code editing, even when only a single programmer is involved.

# M4

The UNIX tool `m4` contains a number of text-editing features (called `macros` and `include`) that could be used to implement IDEs.

# PLs With REGEX and Strings

PLs that contain REGEX and that make string manipulation easy are good candidates for implementing new-breed IDEs.

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
