---
layout: post
title:  "Transpilation 101"
---
Let's choose a very simple language and build a transpiler for it.

Goals:
- transpile to JavaScript
- transpile to Python
- transpile to Common Lisp
- to keep the spec and transpiler down to about 1 page of code (or as close as possible).

We use best-of-breed tricks to make this project as easy as possible:
- Ohm-JS (PEG) parsing for the syntax, like REGEX, but better for transpilation
- one declarative spec that creates code in all target languages (JS, Python, WASM)
- declarative syntax for transpiler-to-target languages
engine to perform code transpilation
- multiple steps (aka pipeline).

Plan:
1. Ohm grammar for the front-end
2. Glue to create OCG intermediate code facts
3. declarative syntax that generates code in all target languages (JS, Python, Common Lisp).

Future:
- extend the language to have scoped blocks in the form `if...then...elseif...else...endif`
- Create 2 syntaxes for the same language - writable, readable. Writable syntax contains lots of syntactic noise that can be easily checked by the transpiler. Readable syntax strips syntactic noise.
- Extend the transpiler to use OCG[^ocg] techniques.

[^ocg]: OCG means Orthogonal Code Generator. Cordy.  Most compiler back-ends are a mish-mosh of various bits of code that produce "portable" code. OCG deconstructed the idea into 2 parts - a generalized back-end plus a declarative MIST walker. OCG uses Data Descriptors and Condition Descriptors for normalization.  The result is a relatively small, declarative, spec for portable code emission.  GCC uses a different form of normalization - RTL pioneered by Fraser Davidson.We should be able use both techniques - OCG to Data Descriptors to RTL - but this was never tried.  OCG and RTL are targeted at CPU instructions in the form of triples (aka "assembler"). The task should become easier when we target HLLs instead of assembler, i.e. when building a transpiler instead of a full-blown compiler.
# Tiny Basic
Let's choose `Tiny Basic` as the language that we want transpile.

Tiny Basic is old and simple, but demonstratesw some of the basic techniques and give us a starting point for hacking.

The steps for building a transpiler are:
1. Write the grammar (using a text editor)
2. Debug the grammar using the [Ohm editor](https://ohmlang.github.io/editor/) and some simple test code,
3. Write a _glue_ template matching the grammar.
4. Write an identity transpiler. Attach rewrites to the _glue_ rules that simply mimic their input.
5. Tweak the identity transpiler to emit the desired code for a given target language.

_Grasem_ is a simple tool that glues an Ohm-JS grammar to a set of _glue_ rules. _Grasmem_ is essentially a glorifed `cat` program.

The full identity transpiler is
```
TINYBASIC {
Basic = Statement+
Statement =   "print" Expr_list -- print
            | "if" Expression Relop Expression "then" Statement -- ifthen
	    | "goto" Expression -- goto
	    | "input" Var_list -- input
	    | "let" Var "=" Expression --let
	    | "gosub" Expression -- gosub
	    | "return" -- return
	    | "clear" -- clear
	    | "list"  -- list
	    | "run"   -- run
	    | "end" -- end
	    
Expr_list = ( string | Expression ) CommaExpr*
CommaExpr = "," (string | Expression) 
Var_list = Var CommaVar*
CommaVar = "," Var
Expression = ("+" | "-")? Term MoreTerm*
MoreTerm = ("+" | "-") Term
Term = Factor MoreFactor*
MoreFactor = ("*" | "/") Factor
Factor =   Var -- var
         | Number -- number
	 | "(" Expression ")" -- paren
Var = "a" .. "z" 
Number = digit+ 
Relop = "<>" | "<=" | "<" | "><" | ">=" | "=" 
string = dq notDQ* dq
dq = "\""
notDQ = ~dq any
}

Basic [@statements] = [[${statements}]]
Statement_print [printkeyword exprList] = [[${printkeyword} ${exprList}]]
Statement_ifthen [ifkeyword e1 relop e2 thenkeyword statement] = [[${ifkeyword} ${e1} ${relop} ${e2} ${thenkeyword} ${statement}]]
Statement_goto [gotokeyword expression] = [[${gotokeyword} ${expression}]]
Statement_input [inputkeyword varList] = [[${inputkeyword} ${varList}]]
Statement_let [letkeyword var eqkeyword e] = [[${letkeyword} ${var} ${eqkeyword} ${e}]]
Statement_gosub [gosubkeyword e] = [[${gosubkeyword} ${e}]]
Statement_return [returnkeyword] = [[${returnkeyword}]]
Statement_clear [clearkeyword] = [[${clearkeyword}]]
Statement_list [listkeyword] = [[${listkeyword}]]
Statement_run [runkeyword] = [[${runkeyword}]]
Statement_end [endkeyword] = [[${endkeyword}]]
	    
Expr_list [stringOrExpression1 @commaExpr] = [[${stringOrExpression1} ${commaExpr}]]
CommaExpr [commakeyword stringOrExpression] = [[${commakeyword} ${stringOrExpression}]]
Var_list [var @commaVar] = [[${var}${commaVar}]]
CommaVar [commakeyword var] = [[${commakeyword]${var}]]
Expression [@plusMinusKeyword term @moreFactor] = [[${plusMinusKeyword} ${term} ${moreFactor}]]
MoreFactor [@plusMinusKeyword term] = [[${pluMinusKeyword} ${term}]]
Term [factor @moreFactor] = [[${factor} ${moreFactor}]] 
MoreFactor [timesDiv factor] = [[${timesDiv} ${factor}]]
Factor_var [var] = [[${var}]]
Factor_number [num] = [[${num}]]
Factor_paren [openParen e closeParen] = [[${openParen} ${e} ${closeParen}]]

Var [c] = [[${c}]]
Number [@digit] = [[${digit}]]
Relop [op] = [[${op}]]
string [q1 @cs q2] = [[${q1}${cs}${q2}]]
dq [q] = [[${q}]]
notDQ [c] = [[${c}]]
```
In _grasem_ you specify an Ohm-JS grammar followed by a _glue_ specification of the rewrites.

The Ohm engine parses the input then calls _glue_ rules that match the parsed portions of the grammar (technically, the parsed nodes form a tree called the `CST`. Most programmers know about `ASTs` which are full trees derived from grammar.  `CSTs` are like `ASTs` but specialized to the actual input program that was parsed. (IOW, an `AST` is tree of what _might_ be matched, whereas a `CST` is a tree of what was _actually_ matched).

Each sub-match in the grammar corresponds to a parameter in the _glue_ rules. (Ohm-JS provides much more detail than we actually need in most real applications. See the Ohm documentation if you want to dig deeper).

The LHS - Left Hand Side - of a _glue_ rule consists of a name followed by a parameter list (in square brackets).

Parameters come in two flavors
1. flat parameters
2. tree parameters.

Flat parameters correspond to captured sub-matches. An analogy would be the `\( ... \)` sub-matches in REGEX.

Tree parameters are multiple flat parameters. Tree parameters line up with `+/*/?` operators in the grammar. There is no direct analogy to REGEX, since a parser can return a bunch of matches (all neatly arranged in a tree or list) whereas REGEX cannot do this kind of thing. It is possible to use `+/*/?` operators in REGEX, but the result returned is the longest string matched by the parameter, whereas in a parser, the result is a list of strings.

For example, roughly, if we match `abcabc` in REGEX using `(abc)+` we get "abcabc". If we match the same thing using a parser, we get two strings "abc" and "abc" (the parser syntax is slightly different in a parser vs. REGEX, too).

The RHS - Right Hand Side - of a _glue_ rule is a rewrite pattern enclosed in double-brackets.  The stuff inside of the rewrite is wrapped in back-ticks and handed to the JS compiler for evaluation as a _template string_. The RHS can contain more detail, e.g. {{ ... }}, but let's skip that for now.

The _template_ is on the LHS (left hand side) of the "=". One rule for each grammar rule. The names must match exactly. When we have "--" grammar rules, we create one _glue_ rule for each variant, named "rule" "_" "variant name".

We use the [Tiny Basic Grammar](https://en.wikipedia.org/wiki/Tiny_BASIC) and modify it (slightly) to suit the requirements of Ohm-JS:
```
TINYBASIC {
Basic = Statement+
Statement =   "print" Expr_list -- print
            | "if" Expression Relop Expression "then" Statement -- ifthen
	    | "goto" Expression -- goto
	    | "input" Var_list -- input
	    | "let" Var "=" Expression --let
	    | "gosub" Expression -- gosub
	    | "return" -- return
	    | "clear" -- clear
	    | "list"  -- list
	    | "run"   -- run
	    | "end" -- end
	    
Expr_list = ( string | Expression ) CommaExpr*
CommaExpr = "," (string | Expression) 
Var_list = Var CommaVar*
CommaVar = "," Var
Expression = ("+" | "-")? Term MoreTerm*
MoreTerm = ("+" | "-")? Term
Term = Factor MoreFactor*
MoreFactor = ("*" | "/") Factor
Factor =   Var -- var
         | Number -- number
	 | "(" Expression ")" -- paren
Var = "a" .. "z" 
Number = digit+ 
Relop = "<>" | "<=" | "<" | "><" | ">=" | "=" 
string = dq notDQ* dq
dq = "\""
notDQ = ~dq any
}
```
## N.B. Left Handles
One of the reasons that BASIC was easy-to-parse (using primitive technologies) was that it's grammar used "left handles". 

Every statement in Tiny Basic begins with a keyword. This makes it easy to parse, even when the parsers were built in an ad-hoc, manual manner.

For example, 
```
let x = 1
```
is an assigment statement in Tiny Basic.

Most modern languages use syntax like
```
x = 1
```
which makes it harder to "know" what is expected next (e.g. when we parse `x`, will we be parsing a statement or a function call `x(...)`?).

LR(k) grammar theory made it possible to declaratively parse syntaxes without the need for left handles, but LR(k) put restrictions on the kinds of languages that could be parsed.

PEG works differently than LR(k) but can parse languages without needing left handles.

PEG uses familiar REGEX-like notation for defining parsing rules.

PEG was introduced in the early 2000's. Until then, most compilers relied on theory-based parser generators like YACC. In fact, we continue to suffer a hang-over from needing to use heavy-handed tools like YACC and continue to believe that building a grammar is _hard_ and needs compiler-building expertise. With PEG, this is no longer true. REGEX used to be a compiler-only technology, but it was built into popular programming languages and was made accessible to many programmers. PEG is beginning to find its way into progamming languages (e.g. Rebol, Racket, etc.)

## N.B. Glue Can't Handle Certain Constructs
In Ohm-JS, we can write
```
Var_list = Var ("," Var)*
```
but, _glue_ can't expand that kind of construct ATM.

We modify the grammar to:
```
Var_list = Var CommaVar*
CommaVar = "," Var
```
This restriction affects the rules `Var_list`, `Expr_list`, `Expression` and `Term`.

[Someday, we will fix this in _Glue_, but we can live with the restriction for now.]
## Ohm-JS Upper-Case Rules
Ohm-JS makes a distinction between rules that begin with an upper-case letter and rules that begin with lower-case letters.

In general, PEG needs to include rules for whitespace (e.g. " ", "\n", "\t", etc.) but Ohm-JS skips[^skip] whitespace if the grammar rule begins with an upper-case letter.

[^skip]: As currently implemented, Ohm will parse "letx = 1" as "let x = 1".  This behaviour can be alleviated by using tokenizing and parser pipelines, but, it requires the grammar progammer to be aware of what is going on under the hood. Ohm has no problem parsing grammars that use commas and semi-colons as separators between identifiers, e.g. "var x, y, z;" instead of "var x y z".

Whitespace recognition adds repetitive "noise" to the grammar.  Most PEGs require explicit handling of whitespace, while Ohm-JS does not require such explicit handling (making Ohm grammars "easier to read").

Note that rule `string` is lower-case in the above grammar, while most other rules begin with upper-case letters. We don't want Ohm-JS to skip whitespace when parsing the insides of a string.
# Light Alpha Testing of the Grammar
Sample statements for evey statement in the grammar.
```
let x = 5
print 5,4,x
if x <> 4 then print 3
goto x
return
clear
list
run
end
```
## Ohm-Editor for Grammar Development and Testing
[Ohm Editor basics](https://guitarvydas.github.io/2021/05/09/Ohm-Editor.html)

[Ohm Editor](https://guitarvydas.github.io/assets/tinybasic.png) for the above grammar and tests.

# Glue / Grasem
## First Pass
Rough-in a partial rule corresponding to every grammar rule (name and parameters, only)
```
...
Basic [@statements] = ...
Statement_print [printkeyword exprList] =  ...
Statement_ifthen [ifkeyword e1 relop e2 thenkeyword statement] =  ...
Statement_goto [gotokeyword expression] =  ...
Statement_input [inputkeyword varList] = ...
Statement_let [letkeyword var eqkeyword e] = ...
Statement_gosub [gosubkeyword e] = ...
Statement_return [returnkeyword] = ...
Statement_clear [clearkeyword] = ...
Statement_list [listkeyword] =  ...
Statement_run [runkeyword] =  ...
Statement_end [endkeyword] =  ...
	    
Expr_list [stringOrExpression1 @comma @stringOrExpression2] = 
Var_list = [var1 @comma @var2] = 
Expression [@plusMinus1 term @plusMinus2 @term2] = 
Term [factor1 @timesDiv @factor2] = 
Factor_var [var] = 
Factor_number [num] = 
Factor_paren [openParen e closeParen] =

Var [c] = 
Number [@digit] = 
Relop [op] = 
string [q1 @cs q2] - 
dq [q] = 
notDQ [c] = 
```
(The above will not compile. It is rough-in only).
## Identity Grammar

# Problems With This Approach
## Statement-Based Instead of Expression Language
## Line Oriented Not Block-Structure Oriented
## Global Variables
## One-Letter Variable Names
## No Recursion
## No First-Class Functions
## No User-Defined Types
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
