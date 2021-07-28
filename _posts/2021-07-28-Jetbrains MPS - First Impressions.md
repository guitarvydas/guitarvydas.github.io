---
layout: post
title:  "Jetbrains MPS - First Impressions"

---

Refer to my essay [Before I Look At It](https://guitarvydas.github.io/2021/07/24/Jetbrains-MPS-Before-I-Look-At-It.html).

In general, I like Jetbrains MPS.

I watched xxx

- Does MPS contain unnecessary complexity?
  - Can I begin using MPS after reading only 1 page or 2 pages of documentation?
    - Nope.
  - I come pre-loaded with DSL-building knowledge - does that help or get in the way,  Maybe I'm "set in my own ways" and will miss a different kind of simplicity
    - Knowing how to build DSLs was probably helpful to me.  JetBrains seems to suggest that domain experts rely on DSL experts to invent DSLs.  I think that this is correct.
- I am wary of claims of *projectional editing* that aren't based on a set of *atoms*.  I guess I'll be looking for atoms.
  - Projectional editing is based on parsing theory.  The *atoms* in MPS are parse-tree nodes.  I think that you need to know parsing theory to understand what is going on. I'm not sure if you need to understand what is going on, though.
- Is MPS "better" than what we've got?
  - Yes.
- Can you build DSLs (SCNs) in a short amount of time?
  - It is not clear to me how steep the learning curve is. I have been polluted by knowledge of how to build languages, compilers, interpreters, DSLs, etc.
- ... tortuous mappings ...
  - MPS provides no assitance here, other than to enable building DSLs.  DSL-builders get better over time.
  - One way out of the tortuous-mapping prison is to build lots of DSLs for a single project (one DSL for every aspect of the project).
- Can you use the DSL to build more DSLs?  (Pipeline of DSLs).
  - Yes, but, you have to supply the plumbing manually.
- Are the Atoms expressible as XML? (XML is triples.)
  - Not sure.  
  - XML is downright ugly.
- DRY - is DRY automated, or does the programmer need to worry about DRY?
  - I didn't see any DRY-help in MPS.
  - Git/Github is *soooo* close to doing DRY automatically.
- Newbies think that a good example of visual programming is a "plus" box, `a = b + c`.  
  - MPS allows tree nodes to be visual things, e.g. tables.
  - I really like that feature.
  - I first saw that feature in Lisp (Lisp lends itself to projectional editing).
- Round trip - Newbies think that round-trip is a good idea.  
  - No attempt at round-tripping in MPS.  
  - Good.
- Not Just Text 
  - MPS can create DSLs that are Not Just Text.
  - Good.
- Layers. 
  - Hmm, I don't think I see any layering-help in MPS.
  - One can create layers by choosing syntax for the DSLs.
  - Enabled, but not enforced.
- Containment.  
  - Same as above - layers.
  - Enabled, but not enforced.
  - Enforcement is a UX issue.
- Java
  - The videos I watched felt outdated because they emphasized Java.
  - It would be better if MPS emphasized the flavor-of-the-day language.  I think that means Python, today.
  - I doubt that MPS is wedded to Java. It should be "easy" to port MPS to emit code in other languages, like Python and JavaScript. (At worst, it should be possible to write an MPS DSL that emits an MPS DSL that emits Python).
- Dialog-based UX
  - Dialogs make a horrible UX 
    - because they want *you* to enter information in the order prescribed by *them*
    - dialogs impede free-form thinking
    - dialogs are a way to allow the underlying technology to cheat, instead of providing layers
    - layers lead to isolation, dialogs, though, flow from the mind-set of "everything at once" (anti-layering)
    - dialogs are, often, like *modes* (see Raskin's "Humane Interface"), esp. when there are more than 7±2 options in the dialog (i.e. the dialog is "flat", TMtTA - too much to think about)
  - Jetbrains MPS seems to use a lot of dialogs

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
