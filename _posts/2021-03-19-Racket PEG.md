Title: PEG  
Author:


Comparison — REGEX vs PEG
   
   (enough to get started)


| REGEX | PEG (Ohm-JS) | Racket (#lang peg) |  |
| :----- | :----- | :----- | :----- |
| /a/ | "a" | 'a' |  |
| /abc/ | "abc" | 'abc' |  |
| /a*/ | "a" * | 'a' * | 0 or more |
| /a?/ | "a"? | 'a'? | optional (0  or 1) |
| /a+/ | "a"+ | 'a'+ | 1 or more |
| /(a)(bc)/ | ("a") ("bc") | ('a') ('bc') | grouping / memo |
| \1\2 | rule: function (v1, v2) { … } | v1:('a') v2:('bc') | naming matches |
| /[a-z]/ | "a" .. "z" | [a-z] | character class |
| /./ | any | . | any |
| /(a|b|c)/ | "a" | "b" | "c" | ('a' / 'b' / 'c') | alternates (original thesis used "/") |
|  | "a" rule | v1:('a') v2:rule | call rule (in context) |
|  | !"a" | ~'a' | not |
|  | rule = … | rule <— … ; | define callable rule |
|  |  | _ | whitespace (convention) |
|  | &"a" |  |  |
|  | addOperation ('…',{ …}) | -> lisp |  |
|  | "{" … "{" … "}" … "}" | '{' … '{' … '}' … '}' | nesting |
|  |  |  |  |

   
   The most interesting differences between PEG and REGEX are

* not
* nested rules

The most interesting difference between Racket #lang peg and Ohm-JS is in the naming of matches.  In Racket (most PEGs) matches are explicitly tagged with variable names in the PEG grammar.  In Ohm, all matches are tagged as parameters to rules in the semantics section.

[In my opinion, the Ohm idea is better.  It leaves the grammar intact and more readable.  One of the problems with REGEX syntax is that it has collected noise over the years, making it even less readable than it originally was.]



PEG vs. YACC
   
   YACC was built from LR(k) theory.  It matches CFG languages.
   
   PEG builds recursive-descent parsers.
   
   PEG can match balanced brackets.  YACC cannot.
   
   YACC is theoretically "more sound".
   
   PEG is more practical.
   
   The main breakthrough in PEG was the idea of using backtracking during the pattern matching.  This used to be a verbotten concept in the late 1900's, but with advances in hardware, the use of backtracking has become practical.
   
   REGEX is also based on theory and is also "sound".
   
   YACC and REGEX produce state machines.
   
   PEG produces a TDPL (top down parser, recursive descent).


Pattern Macthing DSLs

REGEX and PEG are DSLs for pattern matching.

There is little reason to use REGEX instead of PEG, if both are equally available.

For simple, one-line matches, REGEX might be preferred because

* it is available in many tools (e.g. sed, awk)
* it is available in many languages (e.g. JavaScript)
* it has a more succinct syntax for small matches.

REGEX syntax often results in unreadable patterns.

REGEX cannot match nested constructs,[^fn1] for example when matching text in programming languages.

PEG rules are like multiple REGEX patterns that can call each other.  If only one rule is required, REGEX might be a good choice.

In general, though, it is better to use PEG, which allows for later expansion.  When REGEX is grown through maintenance and fixing edge-cases, it usually results in unreadable code.



Racket PEG Documentation
   
   https://docs.racket-lang.org/peg/index.html


Ohm-JS PEG Documentation
   
   https://github.com/harc/ohm



PEG Thesis
   
   You don't need to read this …
   
   https://bford.info/pub/lang/peg.pdf
   


[^fn1]: REGEX probably can be made to match nested constructs, but requires more effort.