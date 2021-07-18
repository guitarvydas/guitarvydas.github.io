---
layout: post
title:  "Brainstorming"
---
Brainstorming is usually associated with creative arts.

Can the ideas of brainstorming be applied to programming?

What does that even mean? 

Isn't programming _Engineering_?

Isn't that the antithesis of art?

Program Design (aka Software Architecture) _is_ an act of creation.

Software Engineering is the activity that comes _after_ Design.  Dot the I's and cross the T's, make sure that all relevant details are understood.

# Engineering Is Not Coding

Note that Software Engineering is _not_ coding[^eng].

See the discussion, below.

# What Do You Need To Brainstorm Software Designs?

- You need the ability to jot ideas down with little resistance
- You need the ability to change your mind with little resistance
- You need to knowing a lot of different things[^know].

[^know]: Different kinds of knowledge allow you to "think outside of the box", i.e. to see different ways to approach the problem-at-hand ; to see similarities of the problem-at-hand to other paradigms. By "different kinds", I don't mean just kinds of programming, but, wildly different kinds of things. Examples from my experience: cooking, astronomy, photography using film and chemicals, wine-making, guitar-playing, trumpet, piano, soldering, wire-wrapping, Physics, EE, swimming, songwriting, etc. etc.

"The more you know, the more creative you can be" (Pat Pattison, songwriting).

# What Inhibits Brainstorming?
Limited scope / knowledge - if all you know is how to use a hammer, everything looks like a nail

For example, if all you know is FP, then everything becomes a function. (This is backwards - focus on the problem first, then find a notation that fits the problem).

Low-level details. [Details Kill](https://guitarvydas.github.io/2021/03/17/Details-Kill.html)

Most current PLs drive at Implementation.  This inhibits thinking about anything but implementation.

Early Lisp tried to allow brainstorming (called Rapid Prototyping back then), but this was beat out of Lisp through the Common Lisp standardization process (the standardization process was agenda-driven: how to make it possible to compile Lisp).

# Layers
Construct thoughts + programs in a layered manner.

Suppress details to a lower layer.

Description of details only flows "downward"

# Discussion: Engineering Is Not Coding
Note that Software Engineering is _not_ coding[^eng].

Implementation is coding.

Software Engineering is the detailed thought process that comes after Software Architecture and before Software Implementation.

[^eng]: Note that "Engineering" is a legal term in some jurisdictions. In Ontario, Canada, it is _illegal_ to use the term "Engineer" to describe someone who isn't certified as an Engineer. Today, we mis-use the term "Software Engineer" to mean anyone who creates _code_. In fact, only a subset of code-creators are true Engineers.  [I know of a case where a company official was contacted and told to stop using the phrase "Software Engineer" in employment advertisements.]

For example, imagine the difference between someone who designs automobiles and someone who repairs them.  If we insisted that our automobiles were repaired only by automobile designers, we would end paying custom rates for repair work (not to mention the possibility that the Designers don't have a lot of experience with using repair tools).

Similarly, I suggest that we divide Software Development into several categories, e.g.
- Software Architecture
- Software Engineering
- Software Implementation
- Software Quality Assurance
- etc.
and pay only for what we need at any point in the process, allowing people to concentrate on activities that they are good at.

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
