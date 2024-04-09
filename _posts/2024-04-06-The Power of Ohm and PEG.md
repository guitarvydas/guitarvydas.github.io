To me, PEG is a DSL for building *parsers*, unlike CFGs which specify *languages*.

It used to be considered obscenely inefficient to use backtracking, but, backtracking works well enough on modern hardware. PEG, and, therefore OhmJS, use backtracking to make specifying *parsers* more convenient. 

We are at liberty to create parsers at the drop of a hat. 

We are at liberty to create many little languages. 

We are at liberty to create new syntaxes in minutes. 

We just need a way to plumb many little languages together to form whole programs. 

We are at liberty to stop using General Purpose Languages and switching to using custom Solution Centric Notations (SCNs). We are at liberty to create a set of SCNs for each project, one or more SCNs for each paradigm employed in a project.

# Skipping
Using OhmJS (and PEG) it is not necessary to specify the complete language to be parsed, due to PEG's ability to recursively parse matched pairs of brackets.

It becomes possible to use OhmJS for "quickies", like inserting test coverage logging into source code by specifying matches for only the interesting constructs, like function definitions, if-then-else, etc.

# Separation of Concerns
Unlike most other PEG libraries, OhmJS separates the grammar code from the semantics code.

OhmJS has no explicit syntax for specifying capture variables. All matches are automatically captured and made available to the semantics code for further processing, or, ignoring.

At first, this sounds "inefficient", but, is a psychological boon to freedom of thought. It's like using a high-level language instead of explicitly writing assembler.

It should be relatively easy to duplicate this feature in other PEGs by writing a preprocessor (in PEG, of course) that splits grammar from semantics.

# Avoiding Niggly Details
OhmJS makes it possible to avoid dealing with niggly details.

This feature encourages programmers to focus on the problem-at-hand instead of notation appeasement.

This is a productivity boon.

# RWR - Term-Rewriting Simplified
I used OhmJS to build a nano-DSL - an SCN (Solution Centric Notation) - that bolts onto Ohm grammars and provides semantics code, without needing to explicitly write semantics code in Javascript.

To enhance simplicity - KISS - RWR is designed to *only* deal with text-to-text ("t2t") transformation.

At first, this sounds less powerful than having the full power of Javascript at your fingertips, but, turns out to be sufficiently useful for building many large projects.

If you squint hard, you can see that the goal of Functional Programming (FP) is to convert programming languages into t2t transformers. Decrees like "no side effects", "assign once", etc. are all aimed at supporting "referential transparency". This goal is trivially achieved (in a hygienic manner) by separating the t2t transpilation process into a separate pre-pass. Tools like `/bin/sh` and `/bin/bash` make this kind of preprocessing transparent. Further research is required, though, to tie generated code back to the original source code, for closing the development environment loop.

# Moore's Law for Software
see 2024-04-06-Moores Law for Software

The above argues that software can be written using many fewer lines of code than is possible with the use of general purpose programming languages.

Ohm, and PEG, are ways to create SCNs - little languages - that drastically reduce written code size.

# How is Ohm Better Than REGEX?

Parsers are better than regular expressions, for scaling pattern matchers.

This is due to the use of push-down finite automata, i.e. stacks and recursion, in full-blown parsers as opposed to relatively "flat" and non-recursive and non-stack-based regular expressions.

Until PEG was invented, parsers were difficult to build. Building a parser turns into a mega-project due to the use of CFG-based technologies.

Before PEG, "recursive descent" parsers were the best way to achieve flexible parsers, but, recursive-descent parsers tended to be ad-hoc and moderately complicated to build. PEG uses backtracking, which makes specification of recursive descent parsing much easier. 

Recursive-descent-like parsing was enhanced with the development of parsing combinators, but, this kind of approach is mired in appeasement of functional programming rules. Ohm, and PEG, are DSLs focused on parsing, whereas parsing combinators are work-arounds that try to straddle, both, parsing and functional programming at the same time. A special purpose DSL is - by definition - more laser-focussed on the target problem (parsing) than a watered-down FP-appeasement approach that uses a general purpose programming language can possibly be.

# Appendix
2024-04-06-Moores Law for Software
# Appendix - See Also

### References

[https://guitarvydas.github.io/2004/01/06/References.html](https://guitarvydas.github.io/2024/01/06/References.html)

### Blog
[blog](https://guitarvydas.github.io/)

### Blog
[obsidian blogs](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx-)
### Videos
[videos - programming simplicity playlist](https://www.youtube.com/@programmingsimplicity2980)
### Pamphlets
[DSL for Writing DSLs](https://tarvydas.gumroad.com/l/hiypq?_gl=1*1bdn1r0*_ga*NTI5MDkzNTI0LjE3MTAzNTQzNjU.*_ga_6LJN6D94N6*MTcxMTQ4ODE0Mi43LjAuMTcxMTQ4ODE0Mi4wLjAuMA..)

[Is Concurrency Difficult?](https://tarvydas.gumroad.com/l/dvtej?_gl=1*o7hy6z*_ga*MjA0NzUyMDY1Mi4xNzA3NDc3MDIx*_ga_6LJN6D94N6*MTcwNzQ3NzAyMC4xLjEuMTcwNzQ3NzI5Ni4wLjAuMA..)
### Discord
[Programming Simplicity](https://discord.gg/Jjx62ypR) all welcome, I invite more discussion of these topics, esp. regarding Drawware and 0D
### Twitter
@paul_tarvydas
### Books (WIP)
[leanpub](https://leanpub.com/u/paul-tarvydas)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
