---
layout: post
title:  "Complexity, Causing Complexity"
---

One form of complexity is caused by flattening dimensions in the Design space.

# Overview
Imagine that we need to write a big application.

The big application has many aspects to it. 

It has many dimensions. 

There are many degrees of freedom in the Design.

We can remove dimensions by flattening them out and expressing them in some sort of LCD (lowest common denominator) language.

We often try keep _all_ of the design details, but we try to express them in only one notation.

The final result is complicated, because the reader needs to un-flatten the notation to be able to understand all of the dimensions of the design.

The reader needs to _reverse engineer_ the notation to recover all of the dimensions.

# Example

## Compiler Pieces
Let's say that we want to write a compiler.

[compiler rough break-down (diagram)](https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-06-01-compiler.png)

We think of the compiler in separate dimensions:

1. The Grammar
2. The Declarations
3. The Uses of Declared Items
4. Code Generation.

Restated: We structure a compiler as follows: 
1. Syntax Analysis
1. Check the incoming program-to-be-compiled for syntax (lexing)
1. Then, check the incoming program for grammar correctness (parsing)
2. Make tables that hold all of the declared items (and their details)
2. Check all of the incoming program-to-be-compiled for declaration-before-use
2. Check for other kinds of errors
4. Emit code.

If we think about the compiler as above, then each step is "easy".

If we schmoo all of the above into one big blob of code, then things get complicated.  Worse yet, maybe they begin to interact. Example: imagine that we make a change in (5) and something in (1) breaks.

Restated for emphasis: if we try to dumb down the design and include _everything_ in one, single, notation, we get a complicated result that is hard to reason about.

The easiest way to think about the above is to keep the steps separated and isolated.

We need _separate_ notations for each of the above steps.  

Restated for emphasis: we want a notation for lexing, another notation for parsing, another notation for detail-gathering, another notation for semantics-checking and another notation for code emitting.

## Denotational Semantics -> Accidental Complexity

Denotational Semantics is an real-life example of how to make the above problem more complicated by using _one language to rule them all_.

Another phrase for this is _accidental complexity_.

Each step is simple on its own. If the steps are combined, then complexity emerges.

## Compiling
We already know how to do lexing.  LEX --> REGEX.

We already know how to do parsing.  YACC, PEG, etc.

We already know how to store semantic information.  Hash tables.

We already know how to check semantics - use the above hash tables.

We already know how to emit code.  Printf(), Javascript template strings, etc, etc. 

Note that the above things are all _separate_ notations.  If we try to schmoo them altogether into an LCD language, they stop being separate and look more complicated than they really are.  If they start to interact (which they invariably do), we get unintended complexity.

# Nesting

Many big wins in computing seem to be related to nesting.

Example, to organize global variables, we nested them --> scoped locals.

Example: to battle spaghetti code, we nested code --> Structured Programming.

Example: To organize data+functions, we nested them --> modules --> OOP.

# Eliding
Q: Is eliding the same as flattening?

A: No.

# 4D mapped to 2D

Flattening is the _projection_ of one dimesion onto others, effectively discarding a dimension.  

I think of problems as being 4D (X/Y/Z/Time) yet I think that code is 2D (X/Y).  

Eliding keeps the dimensions but hides them.

# Design Provenence via Github/diff/etc.
For now, we can use `git` to show diffs from the original Design to any aspect of the design.

In the above example, 
1. We store and edit the grammar on a grammar branch.
2. We do semantic gathering on another branch. I suggest calling it _declare_. 
2. We do semantic checking on yet another branch. I suggest calling this branch _design rules_. Note that _type checking_ falls into this branch.  There might be other things, beyond types, that we would want to check.  (N.B. Haskell sort-of does this.  A function declaration consists of a signature and some code.  Signatures are, effectively, checked in a separate stage.)
3. We do code emission on yet another branch. I suggest calling this _emit_. We might want to optimize the emitted code - that's yet another sub-branch - and so on, ad infinitum (everything is a fractal).

Note that we might edit the grammar in step 1 to help us do step 3, and/or, we might edit the grammar from step 1 to help with step 4, and so on.

The edits in step 3 might be different from the edits in 4. If we try to combine them into a single LCD language, we will get uneccessary complexity.
# Design Provenence Checking
The best way to hang everything together is to ensure that edits are directly related to the original Design.

It would be nice if we could do this automatically, but, for now, we should give someone the job of manually checking provenence (using, say, git and diff) from step 1 to 2, 1 to 2 to 3, 1 to 2 to 3 to 4, and so on.
# Diagrams
The original Design is, often, just a bunch of diagrams on a white board.  Maybe the CEO, who doesn't care about Engineering details, sketched the original Design.

OK - snapshot the diagrams and record provenence.  

The _provenence checker_ ensures that the top level Architecture is directly related to the whiteboard diagrams.  The _provenence checker_ ensures that the Engineering "blueprints" directly relate back to the Architecture. The _provenence checker_ ensures that Implementation directly relates back to Engineering.  The _provenence checker_ ensures that Testing relates directly back to Architecture/Engineering/Implementation/etc. If not, the _provenence checker_ bubbles information back up the chain, checks the change(s) with the next level up and re-jigs the pieces until they all flow from one another without any singularities.

## Automating Provenence Checking
Can we automate _provenence checking_? 

Probably.
## Automating Provenence Using LCD Technology
Can we automate _provenence checking_ by using a single notation for _everything_? 

Probably, but the job becomes more complicated.

# General Purpose Languages
Let's put GPLs in their place.

They are not really _general purpose_, they are tuned for one kind of thought process - _Implementation_.

A lot of languages are tuned for Implementation.



# Example - Relational Languages

This is just an example of the extremes in notation that can arise.

Relational languages break programming up into 2 parts:

- description
- engine (implementation).

The _good parts_ of relational programming are:

- exhaustive search engine

- Syntax for exhaustive search.  

  

PROLOG syntax defines a way to denote _logic variables_ and to denote _rules_.  MiniKanren denotes these same kinds of things differently.

The concept of _printf_ does not really fit the main intent of relational programming.

Q: Can relational languages create formatted output? 

A: Yeah, but I'd rather use _printf_ for formatting output than using PROLOG for such tasks

Formatted output is not the main thrust of relational programming.

The _one-languge-to-rule-them-all_ mentality drives PROLOG implementors into bolting _format_ into PROLOG and, thus, wasting brain power.

The _multi-language/multi-paradigm_ mentality says that it is OK to use PROLOG even if it doesn't create formatted output.  Use PROLOG for exhaustive pattern matching, and use something else (e.g. _printf_ or JS _template strings_ or bash strings) for formatting results.

# Normalization

To do this effectively, we must employ a common _normalized form_ for information (I favor [triples](https://guitarvydas.github.io/2021/03/16/Triples.html) and [factbases](https://guitarvydas.github.io/2021/01/17/Factbases.html]), [factbases 101](https://guitarvydas.github.io/2021/04/26/Factbases-101.html))


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
