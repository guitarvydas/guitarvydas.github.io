---
layout: post
title:  "Two Syntaxes For Each GPL"
---
# Synopsis
Some GPLs (General purpose Programming Languages)[^1]: have syntax that aids the automated syntax checker and some GPLs have syntax that aids the (human) maintainer of the code.

Most GPLs are constrained to using one or other of the syntactic choices, above, with attendant decrease in checkability and/or readability.

The advent of PEG parsing makes it possible to easily create more than one syntax for each GPL, allowing the "best of both worlds" - machine-checkability and human-readability.

[^1]: GPL means General Purpose Programming Language.  Examples would be Python, JavaScript, C++, C, etc.

To inspire development along these lines, I show a small snippet of a DSL and use `Ohm-JS` (and `sed`) to convert from the machine-checkable syntax to human-readable syntax as a simple batch-edit.

It is envisioned that both syntaxes might be presented to programmers in separate windows of their IDEs during program creation.

# Syntax Checking
The programming community learned early how to automatically check for a class of simple errors[^2] by using a technology called *parsers*.

Some GPLs aid parsers by insisting that programmers bracket their code with unique syntax, e.g. `if ... end if`.

Fully bracketed code tends to be verbose and conflicts with programming (maintenance, upgrading, etc.) activity after the programs have been certified by their parsers.

An example of bracketed style syntax would be the Algol/Pascal family of languages.

Other GPLs eschew verbosity and fold all end-brackets to the same, single, character. 

This kind of syntax can be easier for humans to read, since more code first into a programming window.

An example of less verbose syntax would be the C family of languages, and, in the extreme, Lisp (expression) languages and raw assembly code.  For example, in C, all end-brackets are composed of the single right-brace character (`}`).

Using PEG parsing technology, it is possible to create syntaxes easily and quickly.  

There is no reason for GPL designers to choose one kind of syntax over the other, as both syntax styles can be accomodated.

[^2]: Simple syntactic errors are often called *typos*.

# Sample
I show a sample snippet of code written in parsability-style.  

The code itself (nor its correctness) does not matter for the purposes of this article.

What is important is the contrast between the two syntaxes and the tools that were used[^3].

1. I chose to use Ohm-JS augmented by a simple `sed` script to create parsers, and,
2. I chose to use `pfr`[^4] to re-write the code from syntax-1 to syntax-2.

[^3]: This project was completed in less than one day, for both syntaxes and the writing of this article.
[^4]: PFR (parsing find-and-replace) is a simplistic tool that uses Ohm-JS grammars and JavaScript template strings to parse and rewrite text.
## Ohm2 Syntax

Ohm-JS emphasizes keeping the DI[^5] of the original grammar intact.  

Most PEG parsers require the inclusion of "noise" in the parsing rules for parsing whitespace.

Ohm-JS *syntactic rules* allow programmers to skip whitespace and to produce grammars that are otherwise "clean".

Furthmore, Ohm-JS honors separation-of-concerns by separating the grammar rules from semantic rules.

I needed to keep whitespace intact for this project, in particular, I needed to implement the project using Ohm-JS *lexical rules*, which are essentially raw, "noisy" PEG, so that all incoming whitespace would be preserved.

A key observation is that whitespace-recognition appears in grammar rules around terminal constructs (like keywords) and very low-level rules such as *identifier* recognizers.

In Ohm-JS, terminal constructs are written as characters between double-quotes, e.g. ``"end"``.

A new syntax was invented.  The new syntax uses single-quotes for whitespace-preserving terminals. A simple preprocessor maps single-quoted constructs to Ohm-compatible rules.  This new syntax is provisionally called `.ohm2`.

Each such single-quoted construct in Ohm2 syntax, is batch-edited and replaced by a `.ohm`-compatible parsing rule.  

Additional parsing rules are written to support the use of single-quoted terminals, for example 
```
'end'
```
is mapped to 
```
kEnd = "end" ws
```
Currently, these additional rules are written manually.  The added rules are simple.  It is imaginable to generate these additional rules automatically.

Ohm2 syntax looks like Ohm syntax, except that
- many terminals use single quotes, and,
- the syntax portion is followed by a `synonyms:`[^6][^7] portion which is a simple table of mappings (from single-quote syntax to Ohm-compatible rule names).

[^5]: DI means Design Intent
[^6]: Inspired by the TXL language and S/SL.  S/SL preceded TXL.
[^7]: Note that it should be possible to write a pre-pass in Ohm-JS to handle this new syntax and mapping table.

For example, the sample code parser contains a `synonyms:` section like,
```
synonyms:
...
'end'           kEnd
...
'('             kLpar
...
```

This mapping table was converted into a `sed` script.  The `sed` script was created manually in this case, but, might have been generated automatically.

The Ohm grammar contains full rules for the new rules, e.g. `kEnd` and `kLpar` in the above.
#### Outlier - Identifier
There is one non-terminal rule that needs to be manually augmented - the rule for matching identifiers (in this case called `name`).

The modification is the addition of whitespace-recognition suffix to the rule.
# Syntaxes
Below, I list the code snippet and its transformed version.

The original, syntax-checkable syntax, appears as `syntax 1`.

The transformed, less-verbose syntax, appears as `syntax 2`.

When examining the two syntaxes, the reader should observe that `syntax 1` contains fairly verbose syntax, but should produce meaningful messages in the case of simple syntactic errors[^8], and, that `syntax 2` has much of the verbosity stripped away (esp. the `end ...` syntax).

[^8]: Errors in code structure should be more obvious when put in the context of bracketed syntax.

Both syntaxes should be parsable with modern technology.  The difference is in *human readability* vs. *syntax error messages*.

Syntax errors arising out of the use of `syntax 1` should guide programmers to the source of the error(s) quickly, while `syntax 2` allows more code to fit inside a programming window.

Syntax errors arising out of the use of `syntax 2` might produce small mysteries for programmers, since indentation might not correspond to the DI in the presence of typos.

Programmers have learned to cope with such small, syntactic mysteries, *but*, errors that can be caught automatically, and, quickly, can free the programmers' minds to design at higher levels of abstraction.

## Syntax 1
```
object dispatcher
  function dispatch (self : dispatcher  top : asc-container )
    with top
      while ?some-asc-ready
        @transfer-sender-outputs-to-receivers
        with asc = @find-ready-asc
          let message = @pull-message-from-fifo
            @invoke-once-with-message (message)
          end let
        end with
      end while
    end with
  end function
end object

```
## Syntax 2
```
object dispatcher
  function dispatch (self : dispatcher  top : asc-container )
    with top
      while ?some-asc-ready
        @transfer-sender-outputs-to-receivers
        with asc = @find-ready-asc
          let message = @pull-message-from-fifo
            @invoke-once-with-message (message)
```
# Appendix - Sample.ohm2
This code snippet was chosen for its small size, for clarity in this article, and does not represent a full Notation, DSL or GPL.

It should be observed that, in accordance with Ohm's design, the most "interesting" parsing rules are collected together and are not polluted with semantics-checking issues.
```
Notation {
  top = 'object' name
          function+ 
        'end' 'object'

  function = 'function' name '(' formalParameter+ ')'
               statement+
             'end' 'function'

  formalParameter = name ':' type

  statement = withStatement | whileStatement | letStatement | callStatement

  withStatement = 'with' name eqRHS?
                    statement+
                  'end' 'with'

  whileStatement = 'while' expression
                     statement+
                   'end' 'while' 

  letStatement = 'let' name '=' expression
                    statement+
                 'end' 'let' 

  callStatement =   callOperator name '(' actualParameter+ ')' -- withActuals
                  | callOperator name                          -- withoutActuals

  expression = callStatement

    type = name
    callOperator = '@' | '?' 
    actualParameter = name
    eqRHS = '=' expression    

      name = nameFirst nameRest* ws
      nameFirst = letter
      nameRest = alnum | "-"

        ws = whiteSpace*
        whiteSpace = " " | "\t" | "\n"

        kObject = "object" ws
        kEnd = "end" ws
        kFunction = "function" ws
        kColon = ":" ws
        kWith = "with" ws
        kWhile = "while" ws
        kLet = "let" ws
        kAt = "@" ws
        kQuestion = "?" ws
        kLpar = "(" ws  
        kRpar = ")" ws  
        kEq = "=" ws
}

// synonyms:
// 'object'        kObject
// 'end'           kEnd
// 'function'      kFunction
// ':'             kColon
// 'with'          kWith
// 'while'         kWhile
// 'let'           kLet
// '@'             kAt
// '?'             kQuestion
// '('             kLpar
// ')'             kRpar
// '='             kEq
```
# Appendix - Sed Script
```
s/'object'/kObject/g
s/'end'/kEnd/g
s/'function'/kFunction/g
s/':'/kColon/g
s/'with'/kWith/g
s/'while'/kWhile/g
s/'let'/kLet/g
s/'@'/kAt/g
s/'?'/kQuestion/g
s/'('/kLpar/g
s/')'/kRpar/g
s/'='/kEq/g
```
I chose to use `sed` in this project, but, the transformations (batch edits) are simple enough to be performed using any language that supports REGEXPs.
# Appendix - Identity-Sample.glue
In a transformation workflow, I find it easiest to create an identity transformer first, to design and debug the transformer machinery.

Later, the identity transformer is modified for its final use.
```
top [kobject name @Functions kend kobject2] = [[${kobject}${name}${Functions}${kend}${kobject2}]]

function [kfunction name klp @FormalParameters krp @Statements kend kfunction2] =
  [[${kfunction}${name}${klp}${FormalParameters}${krp}${Statements}${kend}${kfunction2}]]

formalParameter [name kcolon Type] = [[${name}${kcolon}${Type} ]]

statement [s] = [[${s}]]

withStatement [kwith name @EqRHS @Statements kend kwith2] =
  [[${kwith}${name}${EqRHS}${Statements}${kend}${kwith2}]]

whileStatement [kwhile Expression @Statements kend kwhile2] =
  [[${kwhile}${Expression}${Statements}${kend}${kwhile2}]]

letStatement [klet name keq Expression @Statements kend klet2] =
  [[${klet}${name}${keq}${Expression}${Statements}${kend}${klet2}]]

callStatement_withActuals [callOperator name klp @ActualParameters krp] =
  [[${callOperator}${name}${klp}${ActualParameters}${krp}]]
callStatement_withoutActuals [callOperator name] =
  [[${callOperator}${name}]]

expression [CallStatement] = [[${CallStatement}]]

  type [name] = [[${name}]]
  callOperator [c] = [[${c}]]
  actualParameter [name] = [[${name}]]
  eqRHS [keq Expression] = [[${keq}${Expression}]]

    name [nameFirst @nameRest ws] = [[${nameFirst}${nameRest}${ws}]]
    nameFirst [c] = [[${c}]]
    nameRest [c] = [[${c}]]

ws [@cs] = [[${cs}]]
whiteSpace [c] = [[${c}]]

kObject [k ws] = [[${k}${ws}]]
kEnd [k ws] = [[${k}${ws}]]
kFunction [k ws] = [[${k}${ws}]]
kColon [k ws] = [[${k}${ws}]]
kWith [k ws] = [[${k}${ws}]]
kWhile [k ws] = [[${k}${ws}]]
kLet [k ws] = [[${k}${ws}]]
kAt [k ws] = [[${k}${ws}]]
kQuestion [k ws] = [[${k}${ws}]]
kLpar [k ws] = [[${k}${ws}]]
kRpar [k ws] = [[${k}${ws}]]
kEq [k ws] = [[${k}${ws}]]

```
# Appendix - Sample.glue
This *glue* script is almost a direct duplicate of the identity transformer script.

Only the `${kEnd}${...}` transformers have been deleted, producing a second syntax on output.

N.B. re. *glue* syntax...  
- Each rule in the script corresponds 1:1 with a rule in the grammar (`sample.ohm`).
- Each *glue* rule contains a parameter list that corresponds 1:1 with sub-patterns in the original grammar.  Parameters that correspond with Ohm *iteratation* rules (`*`/`+`/`?`) must be prefixed by `@`.
- The RHS - right hand side - of each *glue* rule contains a JS *template string* enclosed in double-square brackets `[[...]]` (instead of back-ticks).  In particular, `${...}` syntax evaluates a JS variable (or function in more complicated use-cases) and all other characters are untouched[^18].  The resulting string is `returned` from the semantic function[^19].
- Parameter names used in the RHS are not prefixed (for example, as in the first line, `@Function` appears in the parameter list, but is used as `Function` on the RHS)
- Every *glue* rule creates and returns a single string, by using parameters and hard-coded characters
- *Glue* generates JS code that is used as Ohm-JS *semantics* handling.  *Glue* code only generates and returns strings, which is a subset of the capabilities of general Ohm-JS semantics code.  See Ohm-JS documentation for further details[^10].

[^18]: See JS template string documentation for more details.
[^19]: The Ohm-JS operation, generated by the *glue* tool is called `_glue()`.
[^10]: Semantics code and `return`s are created automatically. The programmer does not need to be concerned with these details.

```
top [kobject name @Functions kend kobject2] = [[${kobject}${name}${Functions}]]

function [kfunction name klp @FormalParameters krp @Statements kend kfunction2] =
  [[${kfunction}${name}${klp}${FormalParameters}${krp}${Statements}]]

formalParameter [name kcolon Type] = [[${name}${kcolon}${Type} ]]

statement [s] = [[${s}]]

withStatement [kwith name @EqRHS @Statements kend kwith2] =
  [[${kwith}${name}${EqRHS}${Statements}]]

whileStatement [kwhile Expression @Statements kend kwhile2] =
  [[${kwhile}${Expression}${Statements}]]

letStatement [klet name keq Expression @Statements kend klet2] =
  [[${klet}${name}${keq}${Expression}${Statements}]]

callStatement_withActuals [callOperator name klp @ActualParameters krp] =
  [[${callOperator}${name}${klp}${ActualParameters}${krp}]]
callStatement_withoutActuals [callOperator name] =
  [[${callOperator}${name}]]

expression [CallStatement] = [[${CallStatement}]]

  type [name] = [[${name}]]
  callOperator [c] = [[${c}]]
  actualParameter [name] = [[${name}]]
  eqRHS [keq Expression] = [[${keq}${Expression}]]

    name [nameFirst @nameRest ws] = [[${nameFirst}${nameRest}${ws}]]
    nameFirst [c] = [[${c}]]
    nameRest [c] = [[${c}]]

ws [@cs] = [[${cs}]]
whiteSpace [c] = [[${c}]]

kObject [k ws] = [[${k}${ws}]]
kEnd [k ws] = [[${k}${ws}]]
kFunction [k ws] = [[${k}${ws}]]
kColon [k ws] = [[${k}${ws}]]
kWith [k ws] = [[${k}${ws}]]
kWhile [k ws] = [[${k}${ws}]]
kLet [k ws] = [[${k}${ws}]]
kAt [k ws] = [[${k}${ws}]]
kQuestion [k ws] = [[${k}${ws}]]
kLpar [k ws] = [[${k}${ws}]]
kRpar [k ws] = [[${k}${ws}]]
kEq [k ws] = [[${k}${ws}]]

```
# Appendix - Bash Script - Run.bash
```
#!/bin/bash
clear
./convert.bash
echo
echo syntax 1...
echo
pfr sample.ash sample.ohm identity-sample.glue
echo
echo syntax 2...
echo
pfr sample.ash sample.ohm sample.glue

```
# Appendix - Bash Script - Convert.bash
```
#!/bin/bash
sed -f synonyms.sed <sample.ohm2 >sample.ohm
```

# Appendix Github
[Two Syntaxes Code](https://github.com/guitarvydas/twosyntaxes)
# Appendix Ohm-JS
[Ohm-JS](https://github.com/harc/ohm)
# Appendix Glue - Transforming Tool
[Glue](https://guitarvydas.github.io/2021/04/11/Glue-Tool.html)
[*This work is fairly new and may contain errors.  The documentation might be incomplete.*]
# Appendix TXL
[TXL](http://txl.ca)
# Appendix S/SL
[S/SL](https://archive.org/details/technicalreportc118univ)
# See Also

[Blog](https://guitarvydas.github.io)
[Table of Contents as of Sept 17, 2021](https://guitarvydas.github.io/2021/09/21/Table-of-Contents-Sept-17-2021.html)
[Videos](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy5)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 