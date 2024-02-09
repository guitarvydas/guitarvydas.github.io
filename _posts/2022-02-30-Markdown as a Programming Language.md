# Markdown As A Programming Language

It is possible to use markdown syntax as a programming language.

This example shows the use of two completely different programming languages bolted together into an executable.

In this particlar example, the following languages are use:
- PROLOG (SWIPL)
- JavaScript
- Bash

The intent of the design (DI) is captured in a succinct manner using markdown-like syntax, then transpiled into Bash and PROLOG and JavaScript code.

The top layer of the succinct program is:
- `#` *name*
- `## parameters`
- `## imports`
- `## query`
- `## display`

PROLOG is used because it contains machinery and syntax for performing queries and exhaustive search.

PROLOG, though - and, relational programming in general - does not encourage easy string manipulation and report generation.  For this purpose, JavaScript (esp. *template strings*) is used.

The transpiler creates temporary source code for PROLOG and JavaScript programs.  The sources are piped together and executed using a shell language (Bash, in this case).

The markdown-like syntax makes it possible to edit the program in markdown editors that were not intended for use as programming editors (like emacs "markdown-mode").

Notably, a good markdown editor can elide sections of the document based on the number of `#`s on the line.  This makes it possible to examine the program in layers "for free", eliding program details to get a sense of the overall design in layered stages.

# Sample Script
```
# connection
## parameters
  Parent
  Edge
  Sender
  Receiver
## imports
  shapes
  names
  connection
## query
  das_fact(kind,Edge,edge)
  sourceof(Edge,Sender)
  targetof(Edge,Receiver)
  das_fact(direct_contains,Parent,Edge)
## display
das_fact(connection, ${Parent}, ${Edge}).
das_fact(sender, ${Edge}, sender{component:"${Sender.component}",port:"${Sender.port}"}).
das_fact(receiver, ${Edge}, receiver{component:"${Receiver.component}",port:"${Receiver.port}"}).

```
## Explanation

The first line `# connection` is *syntactic noise* intended to help the (human) reader understand the purpose of the program.  Note that there is no reason to restrict the contents of that line, since the syntax is based on
## Code
For this discussion, what this code accomplishes is less important than its general structure.

The concept is that the source code (above) is a succinct statement of what was needed for the project, whereas the executable code (below) contains many lower-level details and boilerplate that are required by the corresponding languages.

To transpile the succint code (above) into executable code (below), the transpiler creates two temporary program sources, then pipes the programs together using a simple Bash script.  The Bash script runs the two languages and outputs to *stdout*.

The succinct program uses two technologies:
1. PROLOG to perform exhaustive search and pattern matching
2. JavaScript to format the output results.

The succinct program uses a very simple syntax based on markdown:
- the top level `#` clause contains the name of the succinct program
- second-level `##` clauses contain bits of code in PROLOG and JavaScript.

The second-level clauses are:
- `## parameters`
- `## imports`
- `## query`
- `## display`

In essence, the transpiler uses Bash, PROLOG and JavaScript like assembler.

The resulting, detail-filled code is listed below.  It can be seen that the essence of *what* the program is intended to accomplish is lost in a avalanche of niggly details.  To understand the generated code, the reader must reverse-engineer and "play computer in the head ", then create theories about what the actual programming intention is.

```

temp=temp${RANDOM}
# connection


cat >${temp}.pl <<'~~~'
:- use_module(library(http/json)).
?- consult("fb.pl").
?- consult("/Users/tarvydas/quicklisp/local-projects/eh/das/das2f/shapes.pl").
?- consult("/Users/tarvydas/quicklisp/local-projects/eh/das/das2f/names.pl").
?- consult("/Users/tarvydas/quicklisp/local-projects/eh/das/das2f/connection.pl").
query_helper(Parent,Edge,Sender,Receiver):-
das_fact(kind,Edge,edge),
sourceof(Edge,Sender),
targetof(Edge,Receiver),
das_fact(direct_contains,Parent,Edge),
true.
query:-
(setof([Parent,Edge,Sender,Receiver],query_helper(Parent,Edge,Sender,Receiver),Set),
json_write(user_output,Set,[width(128)])
)
;
json_write(user_output,[],[width(123)]).
~~~
cat >${temp}.js <<'~~~'
const fs = require ('fs');
var rawText = fs.readFileSync ('/dev/fd/0');
var parameters = JSON.parse(rawText);
parameters.forEach (p => {
  var Parent = p [0];
var Edge = p [1];
var Sender = p [2];
var Receiver = p [3];
  
if (true) { console.log (`das_fact(connection, ${Parent}, ${Edge}).
das_fact(sender, ${Edge}, sender{component:"${Sender.component}",port:"${Sender.port}"}).
das_fact(receiver, ${Edge}, receiver{component:"${Receiver.component}",port:"${Receiver.port}"}).`);};
});
  
~~~
swipl -g "consult(${temp})." -g 'query.' -g 'halt.' | node ${temp}.js
rm -f ${temp}.pl
rm -f ${temp}.js

```

# The Transpiler
The transpiler is written in a set of tools based on Ohm-JS.
## Implicit Forall
### Grammar
```
implicitforall {
  main = sharp+ ws+ "query" ws* nl+ match ensure+

  match = line
  ensure = line

  line = ~sharp notNL* nl

  notPAREN = ~"(" ~")" any

    ident = firstChar restChar*
    firstChar = "A" .. "Z" | "a" .. "z" | "_"
    restChar = "0" .. "9" | firstChar
    nl = "\n"
    sharp = "#"
    notNL = ~nl any
    ws = " " | "\t"
}

```

### Glue
```
main [ @sharps @ws kquery @ws2 @nl Match @Ensures] = [[${sharps}${ws}~${ws2}${Match}${Ensures}]]

match [line] = [[${line}]]
ensure [line] = [[(${line.trim ()}->true ; format(user_error,"querythen failed /${line.trim ()}/~n",[]),abort),\n]]

line [@notNL nl] = [[${notNL}${nl}]]

notPAREN [c] = [[${c}]]

ident [firstChar @restChar] = [[${firstChar}${restChar}]]
firstChar [c] = [[${c}]]
restChar [c] = [[${c}]]
nl  [c] = [[${c}]]
sharp  [c] = [[${c}]]
notNL  [c] = [[${c}]]
ws  [c] = [[${c}]]

```

## QD3
### Grammar
```
qd3 {
 Main = Name Parameters Imports Query Display

 Name = sharp line
 Parameters = sharp sharp "parameters" parameter+
 Imports = sharp sharp "imports" import+
 Query = sharp sharp "query" query+
 Display = DisplayClause+
 DisplayClause
   = sharp sharp condKW predicate display -- conditional
   | sharp sharp displayKW display -- unconditional
   | sharp sharp jsonKW            -- json
   | sharp sharp rawKW code        -- raw

 Test = ident "is" string

   parameter = line
   import = line
   query = line
   predicate = line
   display = line+
   code = line+
   message = line+

   line = ~sharp notNL* nl

   condKW = "cond" ws+ commentToEOL -- withcomment
          | "cond" nl               -- nocomment
   displayKW = "display" ws+ commentToEOL -- withcomment
             | "display" nl               -- nocomment
   jsonKW = "json"    ws+ commentToEOL    -- withcomment
          | "json" nl                     -- nocomment
   rawKW = "raw"    ws+ commentToEOL    -- withcomment
          | "raw" nl                     -- nocomment


   commentToEOL = ~sharp notNL* nl

    nl = "\n"
    sharp = "#"
    notNL = ~nl any

    ident = firstChar restChar*
    firstChar = "A" .. "Z" | "a" .. "z" | "_"
    restChar = "0" .. "9" | firstChar
    string = dq notDQ* dq
    dq = "\""
    notDQ = ~dq any
    ws = " " | "\t"
}

```
### Glue
```
Main [Name Parameters Imports Query Display]
= [[
temp=temp\${RANDOM}
${Name}
${Parameters}
cat >\${temp}.pl <<'~~~'
:- use_module(library(http/json)).
?- consult("fb.pl").
${Imports.trim ()}
query_helper(${support.formatParameters ()}):-
${Query.trim ()}
true.
query:-
(setof([${support.formatParameters ()}],query_helper(${support.formatParameters ()}),Set),
json_write(user_output,Set,[width(128)])
)
;
json_write(user_output,[],[width(123)]).
~~~
cat >\${temp}.js <<'~~~'
const fs = require ('fs');
var rawText = fs.readFileSync ('/dev/fd/0');
var parameters = JSON.parse(rawText);
parameters.forEach (p => {
  ${support.formatJSParameters ()}
  ${support.formatConditionalDisplays ()};
});
  ${support.formatFinalDisplays ()}
~~~
swipl -g "consult(\${temp})." -g 'query.' -g 'halt.' | node \${temp}.js
rm -f \${temp}.pl
rm -f \${temp}.js
]]

Name [ksharp line] =    [[# ${line}]]
    
Parameters [ksharp1 ksharp2 kparameters @lines]
  = {{ support.clearParameters (); }} [[]]

Imports [ksharp1 ksharp2 kimports @lines] = [[${lines}]]
  
Query [ksharp1 ksharp2 kquery @lines] = [[${lines}]]

Display [@DisplayClauses] = [[${DisplayClauses}]]
DisplayClause_conditional [ksharp1 ksharp2   condKW    predicate display]
  = [[${support.pushConditionalDisplay (predicate, display)}]]
DisplayClause_unconditional [ksharp1 ksharp2 displayKW           display]
  = [[${support.pushConditionalDisplay ("true", display)}]]
DisplayClause_json             [ksharp1 ksharp2 jsonKW                  ]
  = [[${support.pushFinalDisplay ("true", "\${rawText}")}]]


Test [ident kis s] = [[${ident} === \"${s}\"]]

predicate [line] = [[${line}]]
parameter [line] = [[${support.pushParameter (line)}]]
import [line] = [[?- consult(\"${support.prefix (argv)}${line.trim()}.pl\").\n]]
query [line] = [[${line.trim()},\n]]
display [@lines] = [[${lines}]]
message [@lines] = [[${lines}]]

condKW_withcomment [kcond @ws commentToEOL] = [[${kcond}${ws}${commentToEOL}]]
condKW_nocomment [kcond nl] = [[${kcond}${nl}]]

displayKW_withcomment [kdisplay @ws commentToEOL] = [[${kdisplay}${ws}${commentToEOL}]]
displayKW_nocomment [kdisplay nl] = [[${kdisplay}${nl}]]
jsonKW_withcomment [kjson @ws commentToEOL] = [[${kjson}${ws}${commentToEOL}]]
jsonKW_nocomment [kjson nl] = [[${kjson}${nl}]]

commentToEOL [line nl] = [[${line}${nl}]]
line [@cs nl] = [[${cs}${nl}]]

nl [c] = [[${c}]]
sharp [c] = [[${c}]]
notNL [c] = [[${c}]]

ident [c @cs] = [[${c}${cs}]]
firstChar [c] = [[${c}]]
restChar [c] = [[${c}]]
string [dq @notDQ dq2] = [[${notDQ}]]
dq [c] = [[${c}]]
notDQ [c] = [[${c}]]

ws [c] = [[${c}]]
```


# Appendix - See Also

### References

[https://guitarvydas.github.io/2004/01/06/References.html](https://guitarvydas.github.io/2024/01/06/References.html)

### Blog
[blog](https://guitarvydas.github.io/)

### Blog
[obsidian blogs](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx-)
### Videos
[videos - programming simplicity playlist](https://www.youtube.com/@programmingsimplicity2980)
### Books (WIP)
[leanpub](https://leanpub.com/u/paul-tarvydas)
### Pamphlets
[gumroad](https://tarvydas.gumroad.com/l/dvtej?_gl=1*o7hy6z*_ga*MjA0NzUyMDY1Mi4xNzA3NDc3MDIx*_ga_6LJN6D94N6*MTcwNzQ3NzAyMC4xLjEuMTcwNzQ3NzI5Ni4wLjAuMA..)
### Discord
[Programming Simplicity](https://discord.gg/Jjx62ypR) all welcome, I invite more discussion of these topics, esp. regarding Drawware and 0D
### Twitter
@paul_tarvydas

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
