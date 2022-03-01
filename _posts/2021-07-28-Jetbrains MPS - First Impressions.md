---
layout: post
title:  "Jetbrains MPS - First Impressions"

---

Refer to my essay [Before I Look At It](https://guitarvydas.github.io/2021/07/24/Jetbrains-MPS-Before-I-Look-At-It.html).

In general, I like Jetbrains MPS.

I watched, at least:

[Projectional Editor](https://www.youtube.com/watch?v=iN2PflvXUqQ&t=18s)

[Voice Menu](https://www.youtube.com/watch?v=pVIywLXDuRo)

[Introduction](https://www.youtube.com/watch?v=eEUMAx3g6do&t=1s)



- *Does MPS contain unnecessary complexity?*

  - *Can I begin using MPS after reading only 1 page or 2 pages of documentation?*
    - Nope.
  - *I come pre-loaded with DSL-building knowledge - does that help or get in the way,  Maybe I'm "set in my own ways" and will miss a different kind of simplicity*
    - Knowing how to build DSLs was probably helpful to me.  JetBrains seems to suggest that domain experts rely on DSL experts to invent DSLs.  I think that this is correct.

- *I am wary of claims of projectional editing that aren't based on a set of atoms.  I guess I'll be looking for atoms.*

  - Projectional editing is based on parsing theory.  The *atoms* in MPS are parse-tree nodes.  I think that you need to know parsing theory to understand what is going on. I'm not sure if you need to understand what is going on, though.

- *Is MPS "better" than what we've got?*

  - Yes.

- *Can you build DSLs (SCNs) in a short amount of time?*

  - It is not clear to me how steep the learning curve is. I have been polluted by knowledge of how to build languages, compilers, interpreters, DSLs, etc.

- *... tortuous mappings ...*

  - MPS provides no assitance here, other than to enable building DSLs.  DSL-builders naturally get better over time.  Yes, it is better to use an expert DSL designer.
  - One way out of the tortuous-mapping prison is to build lots of DSLs for a single project (one DSL for every aspect of the project).

- *Can you use the DSL to build more DSLs?  (Pipeline of DSLs).*

  - Yes, but, you have to supply the plumbing manually.

- *Are the Atoms expressible as XML? (XML is triples.)*

  - Not sure.  
  - XML is downright ugly[^1].

  [^1]: Lispers hate XML because XML's syntax is worse than Lisp's.  Lisp has often been accused of having an ugly syntax. 

- *DRY - is DRY automated, or does the programmer need to worry about DRY?*

  - I didn't see any DRY-help in MPS.
  - Git/Github is *soooo* close to doing DRY automatically.

- *Newbies think that a good example of visual programming is a "plus" box, `a = b + c`.*  

  - MPS allows tree nodes to be visual things, e.g. tables.
  - I really like that feature.
  - I first saw that feature in Lisp (Lisp lends itself to projectional editing).

- *Round trip - Newbies think that round-trip is a good idea.*  

  - No attempt at round-tripping in MPS.  
  - Good.
  
- *Not Just Text* 

  - MPS can create DSLs that are Not Just Text.
  - Good.

- *Layers*. 

  - Hmm, I don't think I see any layering-help in MPS.
  - One can create layers by choosing syntax for the DSLs.
  - Enabled, but not enforced.

- *Containment*.  

  - Same as above (see layers).
  - Enabled, but not enforced.
  - Enforcement[^enforce] is a UX issue. Psychology is a strange subject. We *can* write FP code in assembler, but we don't.

[^enforce]: Gentle suggestion is better than force.

- *Java*
  - The videos I watched felt outdated because they emphasized Java.
  - It would be better if MPS emphasized the flavor-of-the-day language.  I think that means Python, today.
  - I doubt that MPS is wedded to Java. It should be "easy" to port MPS to emit code in other languages, like Python and JavaScript. (At worst, it should be possible to write an MPS DSL that emits an MPS DSL that emits Python).
- Dialog-based UX
  - Dialogs make a horrible UX 
    - because they want *you* to enter information in the order prescribed by *them*
    - dialogs impede free-form thinking
    - dialogs are a way to allow the underlying technology to cheat, instead of providing layers
    - layers lead to isolation, dialogs, though, flow from the mind-set of "everything at once" (an anti-layering mindset)
    - dialogs are, often, like *modes* (see Raskin's "Humane Interface"), esp. when there are more than 7±2 options in the dialog (i.e. the dialog is "flat", TMtTA - too much to think about)
  - Jetbrains MPS seems to use a lot of dialogs
- Parsing ASTs
  - One of the videos says that text is always parsed to ASTs and implies that Projectional Editing is the only way out of this rabbit hole and that projectional editing "eliminates" parsing.
  - Parsing is pattern-matching.
  - REGEXP is pattern-matching, but with no push-down stack.
  - PEG is pattern-matching with a push-down stack.
- PEG Pattern Matching
  - Ohm-JS allows pattern-matching of structured text while calling subroutines to perform various tasks with the matching text.
- Parsing to Triples
  - Matches are often represented as ASTs which are often represented as trees.
  - Trees imply structure and, therefore, can limit the imagination on how matches get used.
  - The most fundmental, structure-less representation of matches is as *triples* (Relation, Subject, Object).
  - Trees can be built up from triples, but this requires work.
  - XML is triples, fundamentally.
  - Lisp is triples, fundamentally.
  - Assembler is triples.
- TXL
  - [TXL](2021-12-31-TXL.md) is a pattern-matching tool that creates strongly-typed parse-trees and allows strongly-typed transformations between different kinds of trees, i.e. augmenting languages and tranforming between languages.
- Projectional Editing - Lisp
  - Some Lisp editors are essentially Projectional Editors.
  - Lisp code is RPN triples, a form which lends itself to various syntaxes (I call them *skins*).
  - Lisp macros are a form of projectional editing scripts.
- Smart Editor
  - MPS provides a *smart editor*, where the user (a programmer) cannot write illegal code.
  - I feel that smart editors are a bad idea, since they limit imagination.  Editors (text, diagram, etc.) should allow the user to create *anything* and check it later for legality. Compilers already do this in phases.  Compilers start by lexing the code, then parsing it, then analyzing it for type-safety, etc.
  - Smart editors contain the biases of the original smart-editor-programmer.  Those biases may/may-not fit the problem-at-hand.  I think that the most-general solution is to create triples from pattern-matches.  Triples are problem-agnostic.  Triples are machine-readable (and less human-readable) which means that transformations can be easily automated.  Tree-walkers can be used to automate transformation of trees, but limit the imagination.  For example, UNIX® pipelines got a lot of mileage out of persisting data in a very simple form (lines of text) instead of polluting the data with various structures.

# Conclusion

In general, I like Jetbrains MPS.

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
