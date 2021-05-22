---
layout: post
title:  "Software Components 101 Part 12 Converting Indentation to Nesting"
---
# Synopsis
1. .md -> .block 
2. .block -> .lisp
3. .block -> .brace

[_N.B. We use .lisp only because we have easy access to a pretty printer for .lisp files. This allows us to eye-ball test the interim code._]

# Isolated Stages
We choose to build the diagram transpiler in isolated stages.

We will apply `grasem` over and over until we can process the information using PROLOG facts.

Instead of trying to do everything in one `grasem` file, we will split the work up into small, understandable pieces.

## Example of Isolation - UNIX Pipelines
To get a flavor for isolation, consider UNIX pipelines.

UNIX pipelines provide isolated stages with the restriction that components have 1 input and 2 outputs (stdin, stdout, stderr, resp).

# Steps
## Step 1 The Blocks Grammar
```
MD2BLOCK {

main = line+
line = indent spc toEOL* newline+
indent = "#"+
toEOL = ~newline any

newline = "\n"
spc = " "
}
```
## Step 2 Rough-in Glue Spec
Let's begin the _glue_ code (the 2nd part of the grasem spec) by roughing-in the rules and parameters :
```
main [@lines]
line [block spc @chars @nl]
indent [@octo]
toEOL [c]
newline [c]
spc [c]
```
## Step 3 Create Rewrites for an Identity Grammar
(output is the same as the input)
```
main [@lines] = [[${lines}]]
line [block spc @chars @nl] = [[${block}: ${chars}\n]]
indent [@octo] = [[${convertIndentationToBlockNumber (octo)}]]
toEOL [c] = [[${c}]]
newline [c] = [[${c}]] 
spc [c] = [[${c}]]
```
## Step 4 Create Foreign.js (support code)
[_N.B. I like to put a space between a function and the open paren._]
```
'use strict';
// empty

function resetBlock () {
    scopeAdd ('block' , 0);
}

function convertIndentationToBlockNumber (octoString) {
    return octoString.length;
}

function asNumber (s) {
    return parseInt (s, 10);
}
```
Q: This code should be boring.  Is it?

Q: Even if you don't grok JS, nor use it daily, can you understand what is going on here?  The DI Architect's Responsibility is to make the Design clear to readers.  Is the design clear?

## Step 5 Run and Test MD to Block Conversion
Run.bash:
```
#!/bin/bash
set -e
trap 'catch' ERR

catch () {
    echo '*** fatal error in run.bash'
    exit 1
}

./run-block.bash v
./run-block.bash v-x
./run-block.bash v-x-y
./run-block.bash v-x-y-z

# v/x is the most complicated diagram
cat v-x.block
```

Eye-ball test - it looks OK.  

(It's OK to make mistakes, since we can always start again. We haven't written much code.  The _Design_ remains flexible and hasn't been cast in stone).

# Graduate to the Next Steps
## Step 6 Emit Open and Close Brackets
### Step 7 Emit Open and Close Parens in Lisp
We use Lisp at this stage, because we have easy access to a pretty printer which will allow us to eye-ball the results.

In this case, we use Emacs' `indent-region` command.  Other pretty printers can be used.  Other languages can be used.  We could just eye-ball the results and forego the pretty printing step.

#### MD2Block
```
MD2BLOCK {

main = line+
line = indent spc toEOL* newline+
indent = "#"+
toEOL = ~newline any

newline = "\n"
spc = " "
}

main [@lines] = [[${lines}]]
line [block spc @chars @nl] = [[${block}: ${chars}\n]]
indent [@octo] = [[${convertIndentationToBlockNumber (octo)}]]
toEOL [c] = [[${c}]]
newline [c] = [[${c}]] 
spc [c] = [[${c}]]
```
#### Block2Lisp
```
BLOCK2LISP {

main = line+
line = block ":" spc toEOL* newline+
block = decimalDigit+
decimalDigit = "0" .. "9"
toEOL = ~newline any

newline = "\n"
spc = " "
}

main [@lines] = {{ resetBlock () }} [[${lines}${emitcloseparen (0)}]]
line [block colon spc @chars @nl] = [[${emitopenparen (block)}${emitcloseparen (block)}${chars}\n${shiftblock (block)}]]
block [@digits] = [[${digits}]]
decimalDigit [d] = [[${d}]]
toEOL [c] = [[${c}]]
newline [c] = [[${c}]] 
spc [c] = [[${c}]]
```
#### Run.bash
```
#!/bin/bash
set -e
trap 'catch' ERR

catch () {
    echo '*** fatal error in run.bash'
    exit 1
}

./run-block.bash v
./run-block.bash v-x
./run-block.bash v-x-y
./run-block.bash v-x-y-z


./run-block2lisp.bash v
./run-block2lisp.bash v-x
./run-block2lisp.bash v-x-y
./run-block2lisp.bash v-x-y-z

./run-block2brace.bash v
./run-block2brace.bash v-x
./run-block2brace.bash v-x-y
./run-block2brace.bash v-x-y-z
# v/x is the most complicated diagram
cat v-x.brace
```
#### Run-block2lisp.bash
```
#!/bin/bash
set -e
trap 'catch' ERR
target=$1
catch () {
    echo '*** fatal error in run-blocks.bash'
    exit 1
}

../../grasem/run.bash block2lisp.grasem >_.js
cat _.js foreign.js >_block2lisp.js
node _block2lisp.js < ${target}.block > ${target}.lisp
```
#### Run-block2brace.bash
```
#!/bin/bash
set -e
trap 'catch' ERR
target=$1
catch () {
    echo '*** fatal error in run-blocks.bash'
    exit 1
}

../../grasem/run.bash block2brace.grasem >_.js
cat _.js foreign.js >_block2brace.js
node _block2brace.js < ${target}.block > ${target}.brace
```

# Appendix - Code in Github Repo
[repo](https://github.com/guitarvydas/basicdasl/tree/master/pseudo)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
