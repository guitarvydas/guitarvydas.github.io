---
layout: post
title:  "Jetbrains MPS - Before I Look At It"

---

JetBrains MPS claims to be a tool for building DSLs.

I haven't looked at it yet, but I'm going to.

Let me see if I can capture my thoughts and biases before I become polluted with actual details:

- I think that the current programming culture makes things more complicated than necessary.
  - I'm going to scan MPS for unnecessary complexity
    - Can I begin using MPS after reading only 1 page or 2 pages of documentation?
      - I come pre-loaded with DSL-building knowledge - does that help or get in the way,  Maybe I'm "set in my own ways" and will miss a different kind of simplicity
      - I read a paper once that showed 
        - a) experts (10+ years) evolve patterns and rely on them
        - b) experts can be reduced to being novices if different patterns are used (or, if there are no patterns)
        - experts do/grok things significantly faster than novices (but see (a) and (b) above)

- I am wary of claims of *projectional editing* that aren't based on a set of *atoms*.  I guess I'll be looking for atoms.

- Is MPS "better" than what we've got?

- Can you build DSLs (SCNs) in a few minutes/hours and spend the left-over time thinking about the *problem* instead of worrying about the details of how to make a DSL, how to optimize it, how to DRY[^DRY], etc., etc.

- I think that the current culture is based on a foundation of mathematical thinking, but, mathematics does not describe computing well (it's a mapping from 2D space to 4D space (x,y,z,t)). Mathematics *can* be used to describe computing, but leads to tortuous mappings from 4D space to 2D space.  Mathematicians are a lot like assembler programmers of old (see below).

- Can you use the DSL to build more DSLs?  (Pipeline of DSLs).

- Are the Atoms expressible as XML? (XML is triples.)

- DRY - is DRY automated, or does the programmer need to worry about DRY?

- Newbies think that a good example of visual programming is a "plus" box, `a = b + c`.  This kind of thing is already handled well in existing, textual, GPLs.  Diagrams cannot improve on it.  Diagrams need to be used for "something else". I focus on DI (Design Intent). Text is a poor representation for DI and for networks of components. Diagrams can show this kind of construction better than text can.

- Round trip - Newbies think that round-trip is a good idea.  [Round trip means the ability to recover a diagram from code and v.v.].  IMO, this is a bad idea.  

  - It is hard to build round-tripping into an IDE.  A waste of human brain-power.  It is better to use that left-over brain-power for other things (like DI).

  - Round-tripping was used in the transition from assembler to HLLs.  Assembler gurus claimed that they could produce code that was better than that produced by compilers of the day.  They were right, but, very few programmers possessed such skill.  Then, GCC came along and created code that was as efficient as that produced by assembler gurus.  After the gurus went into retirement, no one bothered to write code in assembler any more.  In fact, no one bothered to look at the code produced by the HLL compilers (an over-simplification: *systems* *programmers* still look at and use assembler.  Average programmers don't.).  

    Ingredients:

    - machine-readable code
    - time (a few years elapsed before compilers could match manually written guru code).

    I'm not even sure that there were any popular round-trip tools that converted between assembler and HLLs.  If there were any such tools, they vanished.  One of the reasons that round-tripping is hard is because compilers generally eradicate information (for example, variable names).  Compilation is mostly one-way - HLL to assembler.  Going from assembler back to HLL is, theoretically, possible,  but hard because the thrown-away information needs to be reconstructed.  The academic field of *design recovery*[^dri] was an attempt at reconstructing DI from code.  It is a lot easier to go one-way, e.g. from DI to code, than to reconstruct information and to recover DI (in a meaninful way).  Actually, it's not so easy to go from DI to code, but it is a *lot* harder to go backwards - hardly worth the effort.

    [^dri]: We used *design recovery* to fix Y2K problems.  This work would have been much easier if the code were written to express Design instead of written only to express computer manipulation.

    Worst of all, round-tripping is a crutch.  If you *think* that you need round-tripping, then you don't believe that the diagram(s) *can* express what needs to be done.  Having used diagrams-to-code for several decades, I feel that the *only* things that diagrams can't express easily are the bits of accidental complexity cruft built into text-only representations, like epicycles, to handle the "edge cases" that text doesn't handle very well (for example, the current manifestation of multitasking and the common belief that multitasking is just a hard problem. Yet, we teach hard real-time multitasking to 5 year-olds[^mt]).

    The belief that diagrams can't work makes you stop polishing the new notation long before it is finished (as finished, as, say, JS or Python).

- Not Just Text - text is good for some things, but programmers (and programmers' bosses) tend to use diagrams first. I would expect to build SCNs (mini-DSLs) using diagams *and* text.

- Layers. I would want to build a solution using layers, choosing any SCN (mini-DSL) that is appropriate for describing each layer.

- Containment.  Some of the biggest *wins* in programming language design have employed containment in some form, e.g. Structured Programming, local variables, etc. Diagrams show containment easily - box B is inside box A. Text is hard-pressed to show containment and resorts to nested curlies {} and/or indentation.  Markdown employs a primitive form of layering (depth/layering is represented by octothorpes `#`). My Chrome and Safari browsers show HTML layering using diagrams. Emacs' `org-mode` provides layer-based ellision, but only on lines of text.

[^mt]: Music notation is a hard real-time notation, complete with timed events and looping.
[^DRY]: DRY means Don't Repeat Yourself.  Present-day programmers are thought to worry about DRY and to apply its principles manually.  DRY should be automated, as part of the IDE and editor and language, etc. Programmers use *diff* for *git* but don't appear to use *diff* for DRY automation.  [_I suspect that part of the problem is the emphasis on human-readable languages instead of machine-readable languages._]

# See Also

[Blog](https://guitarvydas.github.io)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
