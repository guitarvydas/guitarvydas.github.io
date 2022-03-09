---
layout: post
title:  "Parsing BLC"
---
# Elevator Pitch (Synopsis)
I'm working-on/thinking-about a pipeline that macro-expands `λ [[$pair $false] [[$pair $true] $nil]]` into `λ [[ λλλ0 λλ0 ] [[ λλλ0 λλ1 ] λλ0 ]]`, then parses that into executable code in various languages (Python, JS, WASM, sectorlisp, sectorblc, etc., etc.).

WIP.
# Goal
Convert lambda-calculus to code in Python, JS, WASM, etc, etc.

Q: [open question]: does Lambda Calculus / sectorblc / sectorlisp lead to Atoms of Software?

# Simplicity
I am most interested in simplicity.

The goal of `sectorlisp` and `sectorblc` is smallness, with a side-effect of simplicity.

Simplicity and smallness are related, but not necessarily the same thing.

Simplicity is defined as "lack of nuance".

Notational economy is a form of simplicity.

Accountants find that spreadsheets are notationally "simple", but, the notation of spreadsheets is not good enough for theoretical work.

This leads to the question "What is the simplest notation for a given problem?".

If you are using a notation that isn't suited to a problem, you begin to see *tells*.  A tell often manifests itself as statements like "multitasking is difficult". To emphasize, note that a *tell* doesn't mean that a problem is complicated, only that the notation being used is unsuited to describing the problem and results in accidental complexity (aka epicycles).

This question further leads to the observation that there *cannot* be a *single* notation for any sizable problem/solution.  You might choose a notation that is a local minimum, and describes many aspects of the problem/solution, but you end up playing whack-a-mole with the aspects that aren't easily-described by the notation. Clever people (aka "smart" people) often find work-arounds to notational complexity, but, IMO their time would be better-spent thinking about higher-level concepts than figuring out notational work-arounds.

It's "turtles all the way down". Once you find a suitable notation, other suitable simplifications suggest themselves, layered above the suitable notation. Fractally.

For example, chemistry and physics notations are use to describe oxides -> which leads to a notation for semiconductors (transistors and electronics schematics) -> which leads to VLSI -> which leads to assembler -> which leads to HLLs -> which leads to more lambda calculus -> which leads to "The Next Big Thing". Where does internet fit into this?  It doesn't fit well.  We're playing whack-a-mole with internet concepts and saying things like "concurrency is just a difficult problem", and, smart people are finding clever ways to twist the current notation, instead of inventing a better notation.  Maybe The Next Big Thing is a non-stack-based notation for distributed computing.

# Multiple Notations
I believe in choosing the best notation(s) for the job.

Parsers are good for parsing. Parsers are better than, say, parsing combinators, since parsers use (only) a syntax for parsing, without trying to appease GPLs (General Programming Languages).

Relational Programming is good for searching and querying.  In my mind, PROLOG is better than Loops and Recursion for this kind of thing (querying).  Some day, I will try to apply miniKanren to this stuff. (Note that I view core.logic as miniKanren force-fitted into a GPL called Clojure).

The ultimate goal is to compose solutions using many syntaxes and paradigms.

(Note that I, also, think that DaS - Diagrams - is a valid syntax.  We shouldn't be restricted into thinking textual-only.)

I believe in smallness of *notation* ("Does it fit on a T-Shirt?") which isn't necessarily the same as smallness of *code*. HLLs (high level languages) eventually won out over assembler, even though original HLLs produced code that was "worse" than the code produced by assembler programmers.

# Atoms of Software
I think that it is important to take things apart and to strip them down to their bare essentials.

Then, build them back up into "better" development tools, using things like, say, parsers and rewriters (I am not restricted to using parsers and rewriters, but they do look intriguing at the moment).

# Disclaimer
I believe in "showing my work".  This is WIP.
# Contributing
I will gladly impart these ideas to anyone with an open mind - experience not necessary.
# Github
[experiments with parsing blc](https://github.com/guitarvydas/ptblc)
# Prep
I use `prep` which is kinda like `sed` on steroids.

`Prep` uses `Ohm-JS` grammars and `glue` rewriting rules. 

# Usage
See `Makefile`, which uses `run.bash`

# References
[prep](https://guitarvydas.github.io/2022/03/05/Prep.html)
[prep yourube](https://guitarvydas.github.io/2022/01/20/PREP-Tool.html)
[Ohm-JS](https://github.com/harc/ohm)
[sector blc](https://justine.lol/lambda/)
[sector lisp](https://justine.lol/sectorlisp2/)
[glue - see links](https://guitarvydas.github.io/2021/09/15/ABC-Glue.html)

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
