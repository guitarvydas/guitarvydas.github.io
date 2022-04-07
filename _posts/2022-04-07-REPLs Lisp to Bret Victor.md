---
layout: post
title:  "REPLs Lisp to Bret Victor"
---
REPL means "trying things out".

It is derived from the words "Read Eval Print Loop" which were parts of the original Lisp REPL.

## Continuum

REPLs form a continuum
- at one extreme is the programming language REPL of Lisp
- at the other extreme is "Live Programming"

## Bret Victor

IMO, a lot of Bret Victor's independent work boils down to REPLs.

## Rapid Prototyping

Hmm, is *rapid prototyping* just a way to try out designs?

## Dynamic Languages vs. Static Languages

Hmm, *dynamic languages* tend to allow experimentation.

*Static languages* (compilable languages) tend to inhibit experimentation and expect that you already know what you want.

If you don't already know what you want yet, e.g. when starting a new project, compiled languages get in the way of free-form thinking about the problem.

Compilers are optimizers for designs.

Some people argue that type systems - compiler languages on steroids - help them design a problem.  I would argue that *exploring a problem* is Design.  IMO, type systems are but *one* way to *explore a problem*.  

If your problem involves plumbing bits of data together, then types might act as useful models.  

If, on the other hand, your problem involves plugging control-flow bits together, then types might not be the most useful models. Extreme examples of this are lambda calculus[^lc] and continuation-passing style.  The actual unit of pluggability consists of one type - the control-flow-doo-dad (aka function).  

[^lc]: Lambda Calculus is Forth.  Postscript is Forth.  Lambda Calculus is Forth tuned for language theory thinking, postscript is Forth tuned for placing ink dots on pieces of paper.  Forth is atoms.  LC and PS and molecules.

## Waterfall Design

Imagining that you already know what you want, just by *imagining it* and not *trying it out* is the essence of Waterfall Design.

Air Design is like playing Air Guitar.  It sounds perfect in your imagination.

## Primitive REPLs
### Sketches

Artists *try out* art using paper and pencil before commiting to final implementations of the art.

### Songwriting

Songwriters *try out* phrases before commiting to a final form for the song.

See the bus scene in [8 Mile](https://en.wikipedia.org/wiki/8_Mile_\(film\))[^pp] for a graphic example of how one successful songwriter used pen-and-paper as a REPL.

[^pp]: Credit to [Pat Pattison](https://www.patpattison.com) for pointing this out to me.

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