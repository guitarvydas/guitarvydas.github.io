---
layout: post
title:  "Syntax is Frivolous, Paradigms are Essential"
---

Functional thinking leads us to the conclusion that names are meaningless.

I conclude that not only names, but that all syntax is meaningless.

Syntax is frivolous, paradigms are essential.

## Toolbox Languages
Knowing that I can build any syntax in an afternoon makes me think differently about *what* I want in a language.

I want a toolbox of paradigms, not someone else's syntax.

What makes a good toolbox language?
1. machine-readable and machine-writable anti-syntax, I eschew human-readability until the very last moment ; I want to write code that writes code for me
2. snippets that are not tied to a single paradigm.

I want an expression language of triples.

Assembler code consists of triples and allows many paradigms to be use.

What else comes to mind?

Lisp is a good first approximation.  Lisp is an expression language, has almost no syntax and allows many paradigms to be used.

The drawback of Lisp is that you are allowed to use functions that take more than 2 arguments.  Self-discipline is necessary.

Relational programming languages, like PROLOG, can be used, but,
- relational programming languages tend to favour exactly one paradigm (relations)
- self-discipline is necessary to avoid facts (functors) that larger than triples
- relational programming makes simple things - like formatting a string for output - more difficult than it needs to be.

Relational languages are most useful when you want to query a factbase of triples

## Language Design Is Backwards
We continue to use mid-1900 biases when designing languages, e.g. we tend to build languages that are tied to grids of non-overlapping bitmaps.

Today, computers allow us to use something better than "characters" to express languages.

We can use Diagrams[^2].

[^2]: Diagrams as Syntax -> DaS.

We can use SVG.

### SVG To Save The Day

SVG is commonly used to create massive works of 2D art, yet, stripped-down SVG contains the few things we need to replace only-text-characters in programming languages, i.e.
- rectangles
- ellipses
- lines
- text.

## 11th Rule[^1]
Programming languages are IDE wannabes.

[^1]: Apologies to Greenspun and his 10th Rule.

# See Also

(Brainstorming - I believe in brainstorming, the articles below are in that ilk).

[Factbases (aka Triples)](https://guitarvydas.github.io/2021/01/17/Factbases.html)
[Factbases 101](https://guitarvydas.github.io/2021/04/26/Factbases-101.html)
[Triples 2](https://guitarvydas.github.io/2021/03/16/Triples.html)
[Triples in PROLOG](https://guitarvydas.github.io/2021/11/06/Triples-in-PROLOG.html)

[Toolbox Languages 2](https://guitarvydas.github.io/2021/04/28/Toolbox-Languages-(2).html)
[Toolbox Languages](https://guitarvydas.github.io/2021/03/16/Toolbox-Languages.html)

[DaS II](https://guitarvydas.github.io/2021/10/02/DaS-II.html)
[Diagrams as Syntax Is Not Visual Programming](https://guitarvydas.github.io/2021/08/15/Diagrams-As-Syntax-Is-Not-Visual-Programming.html)
[On Diagram Notation](https://guitarvydas.github.io/2021/11/24/On-Diagram-Notation.html)
(See table of contents, "Diagrams" and "DaS")

[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
