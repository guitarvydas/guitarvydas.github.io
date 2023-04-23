Title: Universal Datatype  
Author:

# The Universal Datatype #

The Universal Datatype is a relation, e.g.

relation(subject,object)



# Triples #

Relations are also called a triples.


# Assembler #

MOV R0,R1
is a triple.  

Relation, Subject, Object.


# Normalization #

Data / Code represented as relations is normalized.

Normalization is the most-atomic form of representation.

Example:

rectangle (5, 10, 20, 30)

can be further atomized — normalized — as

rectangle (R1)
x (R1, 5)
y (R1, 10)
width (R1, 20)
height (R1, 30)

[Yes, normalization wastes space and CPU power, but, we have lots of each today.]

# Factbase #

I often use the term fact and put facts into a factbase.

# Compilers #

Compilers like triples, e.g. MOV R0,R1.

# Optimization #

Optimization is easier when target code/data has been normalized.

Peephole optimization is easy to do with even simple tools like awk when code / data has been normalized into triples.

Fraser/Davidson wrote a landmark paper[^fn1] on peepholing which formed the basis of Gnu's gcc.

Normalizing code and optimizing it is not just for compilers.  The techniques could be ratcheted up a notch to cover higher levels of software Architectures.

# Anecdote - Y2K and COBOL #

We analyzed banking source code for Y2K problems.

We used TXL to convert all source code into factbases, then ran backtracking pattern-matching rules over the normalized code.

# Pattern Matching Factbases #

## Backtracking ##

Exhaustive matching can be done with simple algorithms — backtracking.

Backtracking is easier when the data is normalized. 

[That's why compiler writers aim at assembler when writing optimizers.  Today, trees are used, but trees get in the way.]

## PROLOG ##

PROLOG is one of the earliest attempts at backtracking.

[I have built a PROLOG in JavaScript.  See https://guitarvydas.github.io/]

## TXL ##

TXL is a functional, backtracking, parser language.

http://www.txl.ca/


## MiniKanren ##

MiniKanren appears to be the successor to PROLOG-like languages.

MiniKanren can do seemingly-magical things https://www.youtube.com/watch?v=er_lLvkklsk (and https://github.com/webyrd/Barliman).

[One has to wonder what the child of MiniKanren and AI might turn out like.]

# Programming Language Design #

Imagine if all code were normalized to triples.

We'd be programming in assembler, or in the mostly-syntaxless Lisp.

Successive programming language designs have tried to remedy the problems of working in triples, for human consumption.

Programming languages have taken years to design and to perfect.

Now, using PEG parsers, we can build languages in a day[^fn2].  

We can tune a language for a specific problem.  

I call these SCLs — Solution Centric Languages.

## PEG vs. YACC ##

YACC embodies LR(k) theory.

YACC builds languages from the ground up.

PEG builds parsers.

Programmers can understand PEG.  Compiler-writers understand (mostly) YACC.

PEGs are easier to use than YACC.

YACC needs a scanner, e.g. LEX.

PEGs are all-in-one - scanner and parser, utilizing familiar REGEXP-like syntax.


## PEG vs. REGEXP ##

PEG is like REGEXP, only better.

If you use REGEXPs, stop.  

Use PEGs instead.

PEGs make it easy to match sequences that REGEXPs have a hard time with.[^fn3]

# Automation #

Normalization leads to automation.

First, make it repetitive and boring.

Then automate.


# Programming #

Programming consists of two basic activities:

1. breathe in — pattern match
2. breathe out — rearrange and emit.[^fn4]

[If (2) occurs before (1) is finished, we get problems.  FP is an attempt to fix such problems by throwing the baby out with the bathwater.  State is not the problem — unscoped use of State is the problem].[^fn5]


[^fn1]: https://dl.acm.org/doi/10.1145/357094.357098

[^fn2]: Especially if we cheat.

[^fn3]: The difference lies in the fact that PEGs use a stack and allow you to easily write pattern-matching subroutines.

[^fn4]: (2) might also involve actions

[^fn5]: https://guitarvydas.github.io/2020/12/09/Isolation.html.  See, also, Structured Programming, StateCharts, etc.