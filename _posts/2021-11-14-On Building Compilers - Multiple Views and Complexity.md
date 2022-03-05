---
layout: post
title:  "On Building Compilers - Multiple Views and Complexity"
---
# Synopsis
Some problems are large and lend themselves to being viewed from more than one perspective.

Mechanical Engineers know how to create objects using multiple perspectives.  They are taught to make drawings with 3 views:
- Front view
- Top view
- Side view.

Compiler building falls into the multiple-perspective category.  We break down the act of building compilers into at least a few categories, like
- scanning
- parsing 
- semantic checking
- optimizing
- code emitting
- ...

Each *view* of a compiler app tends to need its own paradigm, its own notation, its own DSL.  We have DSL tools for building lexers (e.g. LEX), tools for building parsers (YACC, ANTLR), tools for building code emitters, etc.
# Complexity
One kind of complexity comes from the act of squishing multiple views into a single paradigm, e.g. by using only a single General Programming Language, like Python, Javascript, C++, Haskell, etc.

For example, it is *possible* to build scanners in Assembler, but it is more convenient to use DSLs[^1] to describe scanners in higher-level concepts.

[^1]: Regular expressions are DSLs for describing scanners.

# Rapid DSL Design and Implementation
Currently, it seems to take a long time (weeks, months, years) to build DSLs.

Wouldn't it be nice to be able to slap DSLs together in less than a day?

If such rapidly-designed DSLs don't work well, we should be able to
- rapidly extend them, or,
- throw them away and start again.

### PEG
Parsing Expression Grammars - PEG - are a technology that makes it much easier to design and build DSLs.
#### Ohm-JS and Ohm-Editor
Currently, my favourite PEG is a language called [Ohm](https://ohmlang.github.io).

I use the variant called [Ohm-JS](https://github.com/harc/ohm).

I build up and test grammars using its [Ohm-Editor](https://ohmlang.github.io/editor/).

#### Ohm-Editor
Ohm-editor is like a REGEX tester[^2]

[^2]:[REGEX tester](https://regex101.com).

Ohm-editor gives you a heads-up display of a grammar, test code snippets and the resulting AST[^3] for a given code snippet.

[^3]: Detail: Technically, the displayed tree is a CST.  ASTs break down into two kinds - (1) AST and (2) CST (abstract and concrete, resp.).

This combination makes it very easy to design and debug grammars.

PEG makes it easy to specify grammars.  Ohm-JS + Ohm-Editor is a better PEG toolkit.



# PFR, Glue, Transpilation-Helper
I now build transpilers (source-to-source converters) instead of compilers.

I found that Transpilation is a subset of what Ohm-JS can do.

I found that JavaScript *template strings* are about all that is needed to build most transpilers.

I built several transpilers using Ohm-JS and template strings.

I found myself writing the same code over and over again and, finally, broke down and wrote a light-weight DSL in Ohm-JS for helping me write transpilers. 

That was Glue. It’s a light-weight DSL for writing Ohm-JS semantics code (that focuses on building strings).

After several more iterations, I built [PFR](https://guitarvydas.github.io/2021/10/14/PFR-and-PF.html), which uses Ohm-JS (a subset of Ohm-JS) plus Glue to use the combined capabilities on the command line.

I use bash (or any of the /bin/*sh family) to build pipelines of transpilers. 

I find this to be a productive workflow. For example, I am currently trying to bundle up d2f and f2j - diagram-to-factbase, factbase-to-JSON transpiler tools mostly consisting of bash scripts using PFR, and, some grammars and some semantics (Glue) files.

I suggest that this is a very convenient workflow for building transpilers (but then, I’m biased :-).
# Appendix - History
Parsers fall into two categories:
1. Bottom-Up
2. Top-Down (aka Recursive Descent).

Recursive Descent parsers are easy to build manually.  As the name suggests, recursive functions are used.

Bottom-up parsers are harder to build.  

Tools, like YACC, transform parser specifications into state machines.

Bottom-up parsers can only parse restricted languages.

Bottom-up parsers have the property that they can be analyzed mathematically and various properties can be "proven" about them and the languages that they can parse[^4].

[^4]: The restricted languages are called LR(k) languages.

### S/SL
[S/SL](https://archive.org/details/technicalreportc118univ) (Syntax / Semantic Language) is a DSL for defining top-down parsers.
### TXL
[TXL](2021-12-31-TXL.md) is a functional DSL for layering new syntaxes onto existing languages.
# See Also

[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)
[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC9EJr0nKHwadbHUtc5zHdmQ/videos)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 