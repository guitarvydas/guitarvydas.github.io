---
layout: post
title:  "PEG Again"
---
## Synopsis
1. PEG is a game-changing technology
2. parsing ≣ pattern-matching
3. PEG creates **parsers**, YACC describes **languages** from first principles
4. PEG paper by Bryan Ford

## Discussion
1. Game changing technology
	- allows bowls of syntax approach[^macros], instead of many-years-for-one-language approach
	- PEG, esp. Ohm-JS, allows jail-break from some of the mid-1900s assumptions

[^macros]: Bowls of syntax is known as *macros* to Lispers, but, Lisp macros deal only with lists, not characters. C macros are much more limited and shouldn't be conflated with the Lisp concept.

2. parsing is pattern-matching
	- no magic, parsers are just big pattern-matching programs[^adhoc]
	- PEG is a DSL for pattern-matching
	- REGEX is a DSL for pattern-matching
	- PEG is better than REGEX, because PEG allows subroutines
	- parsing  technology is geared towards parsing text, due to biases and limitations in mid-1900s machines, but, machines have changed

[^adhoc]: Parsers are, hopefully, less ad-hoc than hand-written pattern-matching code.

3. Parsers vs. language first principles
	- subtle difference
	- PEG is a DSL for creating TDPL parsers
	- Language theory ≣ principles of (restricted) language design, can be used to generate parsers, but languages that are parsed are restricted by the theoretical model 
		- model doesn't always reflect reality, but, only what can be conveniently modeled[^nw]
	- PEG allows matching balanced parens, YACC/language-theory/etc. cannot match balanced parens

[^nw]: Notation Worship.  Ironically, sometimes the (insufficient) model is assumed to define reality, and the rest of reality is simply ignored.

4. PEG paper by B. Ford 
	- shows that squishy concepts for top-down parsing[^tdpl] can be theorized and used to build UXs for programmers
	- paper basically shows how to build backtracking for text without using PROLOG
	- uses memoization to avoid re-parsing already-parsed bits

[^tdpl]: TDPL ≣ Top-Down Parsing Language

## Notes & Rambling
1. Game changing technology
	- allows bowls of syntax approach, instead of many-years-for-one-language approach
	- PEG uses backtracking, which used to be verbotten in the mid-1900s
	- PEG is like PROLOG aimed for backtracking over text characters
	- Kleene `*` and Kleene `+` were invented long ago, but not thought to be useful for parsing due to concerns for efficiency ; current computers are magnitudes better than in the mid-1900s -> time to reevaluate basic assumptions, esp. concerns for efficiency
	- PEG allows matching balanced parens, YACC/language-theory/etc. cannot match balanced parens
	- PEG is akin to: automobile vs. walking - changes basic assumptions about what is possible
2. a Parser is just a program, an app
	- REGEX is a simplified form of pattern-matching
	- PEG is a DSL meant specifically for pattern-matching sequences of characters
	- PEG is better than REGEX because PEG allows subroutines
	- PEG is worse than REGEX because PEG specs are usually larger than REGEX specs
	- REGEX syntax is write-only, PEG syntax is more readable (IMO)
	- PEG is like modernized BNF
3. Compiling
	- 1. pattern-match input file
	- 2. make a bunch of tables
	- 3. check input against tables
	- 4. emit code (assembler or other language)
	- typical approach
		- pattern-matcher creates a tree
		- tree-walk the tree to fire "semantic" routines
	- better approach
		- taught at UofT, etc. (Queen's?)
		- syntax-directed compiling
		- build "many" trees, as pipelined, serialized-streams of characters
			- use many parsers to expand & unserialize intermediate trees
			- helps stop tangling of issues and Accidental Complexity
				- unwinds dependencies
				- each step / phase is independent and can be programmed in situ
					- without worrying about causing side-effects in other phases
			- allows compiler-writer to concentrate on one thing at a time
			- similar to pattern-matching in FP languages
				- allow pattern-matching engine to fire functions based on history / sequencing
					- eschew ad-hoc coding of sequence-tracking
				- FP pattern-matching cases on type (and dynamic data?)
				- parsing cases on dynamic data (and dynamic type)
				- OO cases on type
				- PROLOG allows programmer to define "types" in layers ("rules"), then backtracks and performs exhaustive search
				- PEG allows programmer to define layers ("rules") then backtracks
				- miniKanren performs exhaustive match, like PROLOG, without backtracking
				- (backtracking is an attempt at memory optimization - reuse memory by GC'ing it, then trying again, miniKanren doesn't care, it just keeps every possibility on deck as it works)
					- PROLOG algorithm explained in Scheme by [Nils Holm](http://www.t3x.org/bits/prolog-6-code.scm.html)
				- backtracking ≣ inferencing
				- inferencing ≣ exhaustive search
				- has anyone tried to re-cast PEG in miniKanren?
5. beauty of Lisp and Assembler
	- prefix notation
	- very regular -> automatable
		- machines can do the work instead of humans
		- frees up human thinking to consider higher level concepts
	- leads to observation that operators are orthogonal to operands (Cordy's Orthogonal Code Generator)
		- GCC's RTL is a special case of this observation (in RTL *all* operands are registers until the final step)
	- in Lisp, *everything* is an expression, no special syntax for *return* -> regularity (normalization)
	- Lambda Calculus is discovering normalization
	- Sector Lisp (Tunney) is a fine example of the beauty of the FP paradigm
		- my conclusion: bloatware comes from forcing a paradigm to be something it wasn't designed for
		- e.g. FP vs. mutability
			- Tunney's GC is 40 bytes[sic] becase it is pure FP
				- no special cases
				- very few (2) data types - Atoms and Lists
	- Lisp was schizophrenic
		- Lisp tried to serve 2 masters at once
			1. Design
			2. Production Engineering
		- Production Engineering "won out" and warped Lisp (-> Common Lisp, Scheme)
		- REPL is a "natural" outcome of Design-oriented thinking (see Bret Victor, Live Programming - which are REPLs for non-text-based programming)
		- dynamic languages are better for Design, static languages are better for Production Engineering
			- using static languages for Design, inhibits Design
		- Lispworks debugger is better (IMO) than VSCode 
			- Lispworks has more experience
			- dynamic languages -> less trouble to build debuggers than with static languages
6. IMO - data should be OO objects, and, orthogonally, control flow should be syntax
		- flags, state, etc. are not inherently bad
		- unrestricted use of flags is bad, just like unrestricted use of Global Variables is bad
		- wrap syntax *skins* around hoary contructs and never allow users to access them directly
		- Lambda Calculus wraps data items dynamically (on the stack), and, now syntax can wrap stuff that LC is not designed for (using PEG)
		- FP teaches that *variable* names are inconsequential
			- in fact, variables are not variable
		- parsing teaches that *syntax* is equally inconsequential
3. Parser DSL
	- theory is for theoreticians 
		- leads to better languages, but slowly
	- DSL is UX 
		- theoreticians tend to "ignore" UX and don't care if they mangle languages for the sake of correctness 
		- IMO, the ideal is theory -> lint-like tools that preen programmer code, not warp the languages that programmers are allowed to use
		- theory -> helps Production Engineers, hinders Designers 
			- self-editing is "bad"
			- implementation details obfuscate Design
			- implementation details inhibit Design and destroy Design "flow" ("in the zone")
			- biggest advances in CompSci come from eliding and deferring details, e.g. OO, GC, Scoping, Structured Programming, etc.
	- i.e. PEG is for programmers, language theory is for theorists
		- the two don't mix and cannot be combined into a single language
		- PEG allows rapid syntax creation -> one language for programmers, another language for theorists, same bag of paradigms with different syntactic sugar
4. PEG paper by B. Ford -> shows that squishy concepts for parsing can be theorized and used to build UXs for programmers
		- paper basically shows how to build backtracking for text without using PROLOG
		- uses memoization to avoid re-parsing already-parsed bits
		- concerns for efficiency are misplaced
			- based on assumption that programs will grow "big"
			- if you keep programs "small", then efficiency "doesn't matter"
			- IMO: the goal shoud be to keep programs small instead of appeasing bigness
			- I built a PEG without packrat and it worked fine, since, using the new DSL, programs never became big
			- conclusion: when programs become big enough for efficiency to matter, switch notations (create and use a different language)
7. PREP
	- I built a tool using PEG and REGEX that allows me to write pipelined one-liners (in *bash* modulo accompanying grammar and reformat specs)
	- use it to build variants of itself (feed *prep* pipelines with *prep* preprocessors) -> syntax directed transpiling
	- parse diagrams
	- parse .md as a programming language 
		- architectural / Design language
8. See Also
	- Rosie
		- I haven't explored this, but it looks to be in a similar vein (parsing as a tool)
	- Ohm-JS
		- currently, my favourite variant of PEG
		- a DSL for pattern-matching based on PEG principles
		- skips whitespace
			- avoids sullying the grammar with details
		- sends CST (concrete syntax tree - output of parser) to JS for further processing (tree-walking)
		- *every* match is captured (i.e. normalization, no options == good for automation, anti-bloatware)
		- Ohm-JS examples: 
			- T.B.D. 
			- working on book of idioms
			- working on explaining raw markdown parser
			- WASM from arith P.O.C.
			- link to Obsidian raw material ... (will be free)
			- prep
			- Diagrams as Syntax to Python

9 Other
- replace use of REGEX with use of PEG
		- use REGEX for small snippets of pattern-matching
		- use PEG for anything more interesting, esp. structured text (multiline, recursive)
- Programming Languages are IDEs
			- PLs are IDEs for programming (goal === control a machine)
			- PL's based on biases of mid-1900s, e.g. text, concerns for efficiency
			- PEG, esp. Ohm-JS, allows jail-break from some of these mid-1900s assumptions
			- IMO ideal IDE for programming ->
				- choice of notations, text, diagram, hybrid, etc.
				- choice of design rules
					- more specific than type checking
					- tuned to specific project, not generalized
					- PEG allows specializing syntax per project
					- PEG allows many syntaxes for a single project
					- for those who don't want to invent syntaxes -> cookbook
- gaming
	- early games used to be quite econimical
	- bloated now?
	- where did the simplicity go?
		- "it is complicated" is a hand-waving argument, not science
- compiling
	- compiling is akin to sorting Red Smarties into one pile
	- if you can move all operations (of a certain kind) to one pile, then you can pre-operate and save runtime later
	- amortize cost of operations - waste CPU during compile, save CPU later
	- compiling is AKA Production Engineering
		- Software Engineering is more than just Production Engineering


## Disclaimer
I was going for 80% truth and edited out all qualifications for succinctness.


## See Also

[Table of Contents as of Dec. 01 2021](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)
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
