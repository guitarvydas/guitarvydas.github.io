---
layout: post
title:  "DI Refactoring"
---

## Tipping Point

There is a psychological tipping point that affects DI Refactoring[^di].

At some point, there is too much code and the solution becomes "too big to re-engineer".

At that point, *coding* overrides *solving*.  We retain the code and throw away possible improvements.

What is that "tipping point"?

I haven't measured it.

I know that if I use Lisp, I am more likely to throw my code away when I think of design changes.

I know that if I use towers of data structures in just about any PL[^pl] I am more likely to ignore late architectural changes, or, suffer horribly.

I know that if I draw my solution on a whiteboard, I am more likely to accept and implement design changes.[^diagrams]

I know that if I can see my whole solution - say in one eye-full (a window, a page) - then I am more likely to accept and implement design changes.

[^diagrams]: In fact, I have figured out how to automate drawings.  I can make drawings that can be automatically compiled to code.  I favour the use of a minimal subset of SVG as the atomic syntactic element (intead of single characters) - rects, ellipses, lines, text.

[^pl]: PL == Programming Language.

[^di]: DI means _Design Intent_.  Often, the term _Software Architecture_ is overloaded to mean DI.

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
