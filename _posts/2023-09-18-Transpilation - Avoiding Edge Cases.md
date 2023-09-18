
## Overview

I have been thinking beyond "compilers" and working on how to build "transpilers".  Below, I describe a small, niggly problem in the process of transpilation, and how I solved it.

My overall goal is to document how I built a Scheme to JavaScript transpiler for one program - Nils Holm's PROLOG in Scheme converted automatically to JavaScript ("transpilation").  That documentation is on-going and can be found in the repo mentioned below.  

This note describes only a small slice of the transpilation process.

## The Problem

Dealing with edge-cases results in difficulty and bloatware.

We use machines to grok input code.  We call these things *compilers* and *parsers*.

JavaScript requires commas between arguments, except for the last argument.  Treating the last argument specially is an edge-case.  It is easier to write a compiler when such edge-cases are deferred, and, simply cleaned up in the end.  

## A Solution - Normalization

In writing a transpiler from Scheme to JavaScript, I found that it was easier to assume that all actual arguments to functions are terminated by commas.  Such commas, that terminate actual arguments are called *ACommas* in my code.  *ACommas* are denoted by out-of-band Unicode characters "`†`" which are cleaned up in the final pass. 

The transpiler works on input source text.  The transpiler builds up information by inserting more bits of text into the source (instead of building and keeping internal trees, etc.).  The transpiler uses all of the information to convert the text into some other programming language. At the very end of the transpiler chain there's a component that I call `Cleanup`.  `Cleanup` simply removes various tiny character patterns that are not worth dealing with in the grammars, such as converting the string "`,)`" to the string "`)`".

### Chunking and Isolating

Such avoidance of edge-cases is used liberally throughout the transpiler.  

It becomes simpler to reason about such edge-cases when each kind of edge-case is marked up in a unique way. Say, by using unique out-of-band characters.  Once we've figured out what something means, we annotate it and don't re-recognize it in downstream passes, making it easier to reason about sub-tasks in a layered manner.  

We maintain the annotations in some common format, e.g. text.

For example, commas in *formal parameter* lists, i.e. the list of arguments in function *declarations*, are distinct from commas in actual argument lists, i.e. the list of expressions passed to function *calls*.  Formal parameter commas are denoted by "`‡`" characters whereas actual argument commas are denoted by "`†`" characters.  This approach highlights the technique of using text-rewriting in *syntax-driven translation* and is similar to the use of Greek characters and other kinds of short-hand symbols used in mathematical notation, e.g. `Ω`, `ϕ`, `⊥`, `∫`, etc.  

The trick to doing this kind of thing is to find ways of annotating code such that it can be easily parsed later - by Ohm-JS in this case.  Good, thorough parsing removes uses of `if-then-else` from the transpiler code.  The parser decides - automatically - on which control flows are needed.  In FP circles, this is known as *pattern matching*.  In general, the use of `if-then-else` conflated with mutable variables results in code that is difficult to understand, i.e. the code is "unstructured".  OOP eliminates one use-case for `if-then-else` - case-on-type.  Lisp 1.5 uses `COND` to denote the use-case of determining conditional values of functions.  Many other uses of `if-then-else`, though, result in spaghetti logic.

In current practice, a programmer might represent exactly the same information in the form of complicated data structures such as Trees and DAGs.  Expressing this information as text, though, makes it possible to use text-rewriting techniques and "Laws" to manipulate the information.  On the other hand, text annotated in this manner is more difficult for human readers to understand, while posing no difficulties for machines and compilers and transpilers.  Since my task is to build an automated transpiler, I don't care about human-readability, I only care about machine-readability.

Note that the Holy Grail of mathematical notation and of FP (Functional Programming) is to convert all information into normalized form, in most cases textual form.  Personally, I find mathematical notation to be concise, but unreadable, esp. when Greek letters are used.  This is a problem which is similar to that of machine-readability vs. human-readability.  In order to be able to apply "Laws" for transforming bits of equations into other equations, mathematicians must annotate their equations using symbols that are not understood by non-mathematicians.  Trying to read such equations is similar to trying to read the above-mentioned machine-readable-only code - you have to know what certain symbols mean and why they were inserted.  Lay readers don't expect to have to read machine-readable code, nor, do they expect to read mathematical equations written in mathematical notation.

## Non-Text Normalizations

Note that not *all* normalizations are textual.  For example, Feynman developed *Feynman diagrams* to *reason about* certain physical principles in a way that more clearly expressed the ideas being investigated and explained.

## SCNs - Solution Centric Notations

I use the term SCN - Solution Centric Notation - to mean any notation that makes it easier to think about certain problems in certain ways.  

Until recently, it was believed that it would be too difficult to build custom notations for programming.  This belief has resulted in the notion of GPLs - General Purpose Languages.  

With the advent of PEG (Parsing Expression Grammar) technology, though, it has become much easier to create a broad range of nano-DSLs (SCNs) and transpilers.  

Transpiling notations into existing programming language formats makes the task of inventing and implementing SCNs much easier.  SCN builders do not need to write full-blown compilers - they can rely on existing compilers to do the heavy lifting as long as the SCNs are converted into syntax that is compatible with existing compilers.  As a result, it is possible to invent and build SCNs in about one day.  It is now possible to use *many* custom nano-DSLs (SCNs) for each programming project, instead of using one-size-fits-all General Purpose programming Languages.

Currently, it is customary to solve programming problems by building obfuscated SCNs encoded as data structures expressed in GPL notation. An example demonstrating what can be done is in the repo for the evolving[^disclaimer] transpiler project https://github.com/guitarvydas/transpiler.

[^disclaimer]: This project - "transpiler" - is a work-in-progress and is likely to keep changing.  It contains warts and bugs.  I would hope that, at least, the idea of syntax-driven translation is made clear even at this early stage in the project's life.  The code appears to work, most of the current work is that of describing and documenting the goings-on.
## Alan Kay - Next Generation of Expression

The idea of building programming languages on top of existing programming languages is espoused by Alan Kay in https://www.youtube.com/watch?v=fhOHn9TClXY&t=859s where he says, around 31:50, "In a 'real' Computer Science, the best languages of an era should serve as 'assembly code" for the next generation of expression.

## Future

- It should be possible to easily change the transpiler to emit languages other than JavaScript, like Python, Rust, etc.  Odin (a better C) might be the next target.  An intermediate step might be to transpile to Common Lisp.  Common Lisp is only slightly different from Scheme, but, is very different from JavaScript.

- It should be possible to transpile other programs, e.g. miniKanren in Scheme to JavaScript, etc.

- It should be possible to write code in a higher level meta-language and then transpile it to various 3GLs.  A test of this idea might be to convert the 0D code, currently written in Odin and included in the sub-directories `./0d`, `./registry0d`, `./leaf0d`, `./user0d`, `./process` and `./syntax`, to some other language, like Python.

- This drawware0D software contains "`$`" components that directly invoke commands from the shell, in a Unix-like manner.  It is possible to use `draw.io` as a visual shell ("VSH").  More examples of VSH usage might be built.

- Currently, string literals are coded, manually, as components that return strings.  The name of the components begins with single-quote characters.  It should be possible to automatically detect such components and to generate string components, similar in the way the "`$`" components are converted to shell-outs.
## Appendix - Ohm in Small Steps

My first project when learning to use Ohm-JS was a Scheme to JavaScript transpiler.  A "diary" of my progress on that learning curve is https://guitarvydas.github.io/2020/12/09/OhmInSmallSteps.html.

Recently, I dusted off this project and converted it into drawware.  The drawware version of this transpiler forms the playground for this essay.  The repo for the drawware version is (as already mentioned above) https://github.com/guitarvydas/transpiler .

## See Also
### Blogs
- https://publish.obsidian.md/programmingsimplicity (see blogs that begin with a date 202x-xx-xx-)
- https://guitarvydas.github.io/ (up to about mid-2022)

### Videos
https://www.youtube.com/@programmingsimplicity2980
### Books
leanpub'ed (disclaimer: leanpub encourages publishing books before they are finalized)
https://leanpub.com/u/paul-tarvydas
### Discord
https://discord.gg/Jjx62ypR  ("programming simplicity") all welcome, I invite more discussion of these topics
### Twitter
@paul_tarvydas
### Mastodon
*(tbd, advice needed)*

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
