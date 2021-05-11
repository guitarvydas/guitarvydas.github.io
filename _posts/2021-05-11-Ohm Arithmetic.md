---
layout: post
title:  "Arithmetic Example in Ohm-JS and grasem"
---
# Introduction
This essay discusses how to build the simple "Arithmetic" example found in 
[Ohm-JS](https://github.com/harc/ohm/tree/master/examples/math).

We create an identity grammar.

We create code for Python and JS and Lisp from the specification.

We discuss the difference between upper-case and lower-case grammar rules.
# Basics
Ohm-JS is a PEG parser library (it calls itself a language).

PEG is a lot like REGEX, but better.  

PEG is easy to use and can match things that REGEX can't match (in fact, PEG can match things that other parsers can't match).

Ohm-JS is my (current) favorite version of PEG for 2 main reasons:

1. The grammar remains pure and readable.  The code for doing-something with the matches does not go in the grammar, as it does in most other PEG tools that I've seen.
2. The [Ohm-Editor](https://ohmlang.github.io/editor/) makes it very easy to develop and debug grammars.  PEG is already good for developing grammars, but Ohm-Editor is maybe 10x better than even PEG.  I usually spend about a day or two debugging PEG grammars, but with Ohm-Editor I measure development time in 10's of minutes.

[Ohm](https://github.com/harc/ohm)

We use the same grammar to generate code in the 3 languages.

# GRASEM and GLUE
I developed a tool that I call _glue_ to dovetail with Ohm-JS.

_Glue_ generates the what-to-do-with-the-matches code for Ohm-JS.  (Ohm-JS calls this "the semantics" and expects us to program it in JavaScript).

_Grasem_ is a micro-tool that joins an Ohm-JS grammar together with a _glue_ specification into one file (a .grasem file).  (Guess what?  The _glue_ tool was developed using Ohm-JS.)

With _grasem_, we can write a transpiler - using only simple operations - and not touch JS at all.

Briefly - a _glue_ spec consists of one rule for every rule in the grammar.  The name of the rule must be the same as the name used to name a grammar rule.  The LHS of a _glue_ rule takes one parameter for each partial match in the grammar rule (the match can be a single match or a tree-match, with slightly different syntax for each kind of parameter).  The RHS of a _glue_ rule consists of an optional chunk of JS followed by an output format (using the JS back-tick syntax).  _Glue_ also allows the programmer to create a set of scoped (inherited) variables that annotate the tree-walk.  A _glue_ rule recursively walks the CST (concrete, not abstract, syntax tree) built by the Ohm-JS grammar and outputs code as per the specification.

The _glue_ syntax is meant for machine-readability instead of human-readability.  (Hint: Someone might want to create a more human-readable syntax, using, of course, _Ohm-JS_ or _glue_ or _grasem_).

[Glue Manual](https://guitarvydas.github.io/2021/04/11/Glue-Tool.html)

[Grasem Documention](https://guitarvydas.github.io/2021/04/11/Grasem.html)
# Identity Grammar
The first step in developing a grasem program is to write the grammar using the Ohm-Editor.

The second step is to create _glue_ code that outputs the input - exactly.  Most parser technologies strip and discard whitespace at an early stage.

An example of these two steps can be seen in commit 5dd6c3df5a31e19cc09a7ff3ea3192a0eeb57976 of [arithmetic identity](https://github.com/guitarvydas/arithmetic).

This set of 2 steps - creating an identity transpiler - produces a working a grammar and an output spec.

In subsequent steps, the programmer hacks on the output spec to perform desired manipulations.

In this (simple) example, I cloned the _grasem_ spec 3 times and hacked on the _glue_ specs of each clone to produce Python, JS and Lisp code.  The final result is in [my github arithmetic repo](https://github.com/guitarvydas/arithmetic).
# Upper-case vs Lower-case
Ohm-JS tries to improve grammar readability by skipping over whitespace.

In Ohm-JS, rules that begin with capital letters, perform automatic whitespace skipping.

Ohm-JS rules that begin with lower-case letters work like PEG, requiring the programmer to specify matches for whitespace.

PEG, unlike other parsing technologies, allows programmers to write, both, the scanner and the parser in the same language (for example, to use YACC, you need to provide a LEX scanner - YACC and LEX are two completely different things with separate syntaxes).  This feature makes PEG more accessible to non-compiler-writers, but, it means that grammars are sullied by the addition of whitespace sub-rules.

If one is concerned more with machine-readability than with human-readability (as I am), then this feature is of little help.

When one writes grammars for languages that use commas and semi-colons (`,` and `;` resp), this Ohm-JS feature is a time-saver, but, when one writes grammars for comma-less languages, this feature can cause strange behaviour ((you don't need to understand this point to be able to just-use Ohm-JS - e.g. "two words" is matched as one word "twowords".  The secret to dealing with this kind of problem is to use tokens, or, to create a list of delimiters in the grammar, or, to build grammars in a staged manner (the first stage is written using only lower-case rules)).

# Arithmetic in 3 Languages - Python, JS and Lisp
The 3 language transpilers are invoked by running `.bash` scripts:
```
arithmetic % ./pyrun.bash 
9.11111111111111
7
123
42
arithmetic % ./jsrun.bash
9.11111111111111
7
123
42
arithmetic % ./lisprun.bash
82/9
7
123
42
arithmetic % 
```

# WASM
Wasm is next.

# Dissection
Let's look at pymath.grasem.

Let's look at the bottom-most grammar rule (the middle of the file, just before the closing `}`):
```
  number  (a number)
    = ...
    | digit+             -- whole
```

The grammar rule says that a whole number is `digit+`.  PEG uses syntax that is similar to REGEX, for example `digit+` means `match 1 or more digits`.  Digit is a built-in rule that comes with out-of-the-box Ohm-JS.  `+` means 1-or-more, whereas `*` means 0-or-more and `?` means optional (0 or 1).  

The comment in the parentheses `(a number)` is used only during the creation of parse-error messages and is ignored in successful parses.

The `number` grammar rule is broken into two branches
1. the `-- fract` branch
2. and the `-- whole` branch

Each branch is named by the rule name and the branch name, e.g. `number_whole` in this case.

(Notice that the branches are "uneven" in match length.  The `number_fract` branch matches 3 things - "digit*" and "." and "digit+".  The `number_whole` branch matches only 1 thing - "digit+".  That is why we need separate sub-names for the branches).

The _glue_ section contains a matching rule
```
number_whole [@n] = [[${n}]]
```

This rule says that `number_whole` takes one parameter `n` and that it is a tree parameter `@n` matching up with `digit+` (`*`, `+` and `?` are tree parameters).

The RHS of this _glue_ rule gives the rewrite surrounded by double-brackets
`[[${n}]]`.  The RHS says to make the variable `n` into a string and to return that string.  See JS back-tick string documentation for further information on how to format the RHS.

OTOH, the AddExp_plus rule is
```
AddExp_plus [e1 op e2] = [[${e1}+${e2}]]
```
which says that AddExp takes 3 parameters (e1, op and e2), none of which are tree parameters.  The rewrite is fairly simple - make e1 and e2 into strings and stick a `+` character between them.  

## Rabbit Hole
Basically, anything inside the dollar form `${ ... }` is evaluated (by Javascript), whereas everything else is just copied to the output string.

_Glue_ does almost no work here.  _Glue_ just wraps back-ticks around the rewrite string and relies on JS to do the actual work.  We transpile the _.grasem_ spec into a .js file and then run the JS file (using node.js).  See the pyrun.bash file.  You can view the generated intermediate file by looking at `_pymath.js`.  `_pymath.js` is a _JS app_ that _creates_ a python program - see `_temp.py`.

### Deeper Rabbit Hole
Aside: this example is quite simple - the _glue_ rules consist of `name [ parameters ] = [[rewrite]]`.  There is no optional JS on the RHS (optional JS would be enclosed in double-braces)).





<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
