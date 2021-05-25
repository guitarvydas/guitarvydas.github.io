---
layout: post
title:  "Software Components 101 - Part 14 Checking The Rewrite"
---
# Synopsis

We changed our minds and decided that we should enter the diagrams in a more basic level.

This change has freed us to write the components in a programmers' editor (in this case Emacs, using org-mode).

We used `markdown` syntax to express diagrams.

We have decoupled all domain knowledge from the diagrams.

We have kept the existing diagrams, but have re-entered their data using primitives:
- rects
- rounded rects
- circles
- text
- arrows.

We allow diagram objects to have attributes, like
- color (green, yellow, red)
- stroke-width (1, 3)
- shape rounded _(for rects only)_

We have decomposed the diagrams into separately compiled sub-diagrams.  For example, the diagram "v" now consists of 4 diagrams - "v", "v/x", "v/x/y" and "v/x/y/z/" (see the [draw.io diagram](https://github.com/guitarvydas/basicdasl/blob/master/pseudo/kernel.drawio).

# Facts
The generated facts are:

- contains(ID,CID).
- synonym(ID,_name_).
- rect(ID,nil).
- circle(ID,nil).
- ellipse(ID,nil).
- text(ID,SID).
- str(SID,_"string"_).
- arrow(ID,AID).
- sendersynonym(AID,_name_).
- receiversynonym(AID,_name_).
- rounded(ID,nil).
- color(ID, _{green | yellow | red}_). 
- strokeWidth(ID, _{1 | 3}_).

# 5 Sub-Tasks
We want to convert diagrams from .md format into .pl format (markdown to PROLOG facts).

We do this in 4 steps.
- .md->block numbers (.block)
- .block->.brace
- .brace->.fb
- .fb->.pl

See `run.bash` for details.

We add a step .block->.lisp to help with eye-ball debugging early in the process.  We use a Lisp pretty printer (in this particular case `emacs`+`lisp-mode`+`indent-region`) to format the code allowing to manually (eye-ball) check the .block file for data entry errors (some errors were found).  

After an initial check, we skip the .block->.lisp step and use only the .block->.brace step.

## Steps 1 & 2 - Converting Indented Lines to Bracketed Lines
The main problem (converting .md input to .pl input) begins with conversion from indented .md format to bracketed (open brace ... close brace) format.

This is essentially the same as converting Python indented code to bracketed code.

We divide this step into 2 sub-tasks
1. prefix each line with a block number
2. insert opening and closing braces where the block number changes.

At first, we are compelled to perform both tasks, 1 & 2, in the same step.  We deconstruct tthe task into two - very simple - steps which.  This helps make the design (painfully) clear.  The combined version needs to (1) keep track of indentation and (2) needs to calculate where to insert braces. Attempting to solve both sub-tasks in one task leads to complication and lack-of-understandability. Splitting these two sub-tasks into isolated pieces is easy using Ohm-JS.  There is a good reason to split the task into two sub-tasks - splitting makes the Design more clear and obvious. There is no good reason _not_ to split the task, but, programmers are usually trained to manually worry about efficiency and feel compelled to create a more-complicated solution ; efficiency concerns are the _only_ reason to not split this task (and they cite "obviousness" as a justification).  This example is extremely small, yet shows two clear sub-divisions, which can easily be composed using a pipeline. Corollary - if pipelines are too inefficient to be used in this simple example, then we should attack the eifficiency issue head-on, instead of making trade-offs in the Design phase.  At one time, subroutines (CALL/RETURN using stacked parameters) were thought to be too inefficient for practical application[^balr].

[^balr]:In fact, early IBM 360's had no CALL/RETURN instructions baked into the CPU.  It was thought that pushing parameters onto a stack (instead of using registers) and changing the program counter (twice) was too inefficient. If one really wanted to employ such inefficient code, one would use the BALR instruction and create a linked-list instead of using a baked-in stack.  Note that changing the Program Counter affects instruction pipelines.

See `run-block.bash` and `md2block.grasem` for the conversion of indentation into block numbers.

## Step 0 The V.MD file
```
# rect v
## shape rounded
## color F5F5F5FF
## circle v/a
## circle v/d
## rect v/b
### text "make empty runnable"
### shape rounded
### rect v/b/a
#### color green
### rect v/b/b
#### color green
## ellipse v/c
### text "empty runnable"
## rect v/x
### color E3E3E3FF
### shape rounded
### rect v/x/a
#### color green
### rect v/x/b
#### color green
### rect v/x/c
#### color yellow
## arrow v/a v/x/a
## arrow v/a v/b/a
## arrow v/b/b v/c
## arrow v/c v/x/b
## arrow v/x/c v/d
```

## Step 1 Convert .MD Indentation to Block Number
The v.md file is converted to a v.block file:
```
1: rect v
2: shape rounded
2: color F5F5F5FF
2: circle v/a
2: circle v/d
2: rect v/b
3: text "make empty runnable"
3: shape rounded
3: rect v/b/a
4: color green
3: rect v/b/b
4: color green
2: ellipse v/c
3: text "empty runnable"
2: rect v/x
3: color E3E3E3FF
3: shape rounded
3: rect v/x/a
4: color green
3: rect v/x/b
4: color green
3: rect v/x/c
4: color yellow
2: arrow v/a v/x/a
2: arrow v/a v/b/a
2: arrow v/b/b v/c
2: arrow v/c v/x/b
2: arrow v/x/c v/d
```
The grasem code to convert v.md to v.block is:
```
MD2BLOCK {

main = line+
line = indent spc toEOL* newline+
indent = "#"+
toEOL = ~newline any

newline = "\n"
spc = " "
}

main [@lines] = {{ resetBlock (); }} [[${lines}]]
line [block spc @chars @nl] = [[${block}: ${chars}\n]]
indent [@octo] = [[${convertIndentationToBlockNumber (octo)}]]
toEOL [c] = [[${c}]]
newline [c] = [[${c}]] 
spc [c] = [[${c}]]
```


## Step 3 Converting .block to .brace
The above v.block file is converted to v.brace:
```
 {
 rect v
  {
  shape rounded
  color F5F5F5FF
  circle v/a
  circle v/d
  rect v/b
   {
   text "make empty runnable"
   shape rounded
   rect v/b/a
    {
    color green
   }

   rect v/b/b
    {
    color green
  }
}

  ellipse v/c
   {
   text "empty runnable"
  }

  rect v/x
   {
   color E3E3E3FF
   shape rounded
   rect v/x/a
    {
    color green
   }

   rect v/x/b
    {
    color green
   }

   rect v/x/c
    {
    color yellow
  }
}

  arrow v/a v/x/a
  arrow v/a v/b/a
  arrow v/b/b v/c
  arrow v/c v/x/b
  arrow v/x/c v/d
}
}
```
[N.B. Formatting doesn't matter to the computer, as long as the notation can be parsed by the computer.  Formatting this intermediate file is only useful for producing a human-readable result.  We are using automation and don't care about human-readability].

The block2brace.grasem code is:
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

main [@lines] = {{ resetBlock () }} [[${lines}${emitclosebrace (0)}]]
line [block colon spc @chars @nl] = [[${emitopenbrace (block)}${emitclosebrace (block)}${spaces (block)}${chars}\n${shiftblock (block)}]]
block [@digits] = [[${digits}]]
decimalDigit [d] = [[${d}]]
toEOL [c] = [[${c}]]
newline [c] = [[${c}]] 
spc [c] = [[${c}]]
```
The foreign functions emitopenbrace and emitclosebrace can be found in the repo [foreign functions](https://github.com/guitarvydas/basicdasl/blob/master/pseudo/foreign.js

## Step 4 Converting Bracketed Lines Into Facts
This step converts the above `v.brace` file into `v.fb`:
```
rect v_0 nil
synonym v_0 v
rounded v_0 nil
color v_0 F5F5F5FF
contains v_0 v_1
circle v_1 nil
synonym v_1 v_a
contains v_0 v_2
circle v_2 nil
synonym v_2 v_d
contains v_0 v_3
rect v_3  nil
synonym v_3 v_b
contains v_3 v_4
text v_4 nil
str v_4 "make empty runnable"
rounded v_3 nil
contains v_3 v_5
rect v_5  nil
synonym v_5 v_b_a
color v_5 green
contains v_3 v_6
rect v_6  nil
synonym v_6 v_b_b
color v_6 green
contains v_0 v_7
ellipse v_7 nil
synonym v_7 v_c
contains v_7 v_8
text v_8 nil
str v_8 "empty runnable"
contains v_0 v_9
rect v_9  nil
synonym v_9 v_x
color v_9 E3E3E3FF
rounded v_9 nil
contains v_9 v_10
rect v_10  nil
synonym v_10 v_x_a
color v_10 green
contains v_9 v_11
rect v_11  nil
synonym v_11 v_x_b
color v_11 green
contains v_9 v_12
rect v_12  nil
synonym v_12 v_x_c
color v_12 yellow
contains v_0 v_13
arrow v_13 nil
sendersynonym v_13 v_a
receiversynonym v_13 v_x_a
contains v_0 v_14
arrow v_14 nil
sendersynonym v_14 v_a
receiversynonym v_14 v_b_a
contains v_0 v_15
arrow v_15 nil
sendersynonym v_15 v_b_b
receiversynonym v_15 v_c
contains v_0 v_16
arrow v_16 nil
sendersynonym v_16 v_c
receiversynonym v_16 v_x_b
contains v_0 v_17
arrow v_17 nil
sendersynonym v_17 v_x_c
receiversynonym v_17 v_d

```

The main actions in this step are: 
- to parse the .brace file, 
- then walk the resulting parse tree (a CST) 
- keep track of dynamic scope using `pushNewObject()` creating parent-child relationships emitting `contains` facts.

The output is a triple per line.

## Step 5 Converting .fb to .pl
A simple grasem file converts triples to PROLOG format (`r s o` -> `r(s,o).`).

Then, UNIX `sort` is used to group rules together (required by PROLOG).

The final output v.pl is:
```

arrow(v_13,nil).
arrow(v_14,nil).
arrow(v_15,nil).
arrow(v_16,nil).
arrow(v_17,nil).
circle(v_1,nil).
circle(v_2,nil).
color(v_0,"F5F5F5FF").
color(v_10,"green").
color(v_11,"green").
color(v_12,"yellow").
color(v_5,"green").
color(v_6,"green").
color(v_9,"E3E3E3FF").
contains(v_0,v_1).
contains(v_0,v_13).
contains(v_0,v_14).
contains(v_0,v_15).
contains(v_0,v_16).
contains(v_0,v_17).
contains(v_0,v_2).
contains(v_0,v_3).
contains(v_0,v_7).
contains(v_0,v_9).
contains(v_3,v_4).
contains(v_3,v_5).
contains(v_3,v_6).
contains(v_7,v_8).
contains(v_9,v_10).
contains(v_9,v_11).
contains(v_9,v_12).
ellipse(v_7,nil).
receiversynonym(v_13,v_x_a).
receiversynonym(v_14,v_b_a).
receiversynonym(v_15,v_c).
receiversynonym(v_16,v_x_b).
receiversynonym(v_17,v_d).
rect(v_0,nil).
rect(v_10,nil).
rect(v_11,nil).
rect(v_12,nil).
rect(v_3,nil).
rect(v_5,nil).
rect(v_6,nil).
rect(v_9,nil).
rounded(v_0,nil).
rounded(v_3,nil).
rounded(v_9,nil).
sendersynonym(v_13,v_a).
sendersynonym(v_14,v_a).
sendersynonym(v_15,v_b_b).
sendersynonym(v_16,v_c).
sendersynonym(v_17,v_x_c).
str(v_4,"make empty runnable").
str(v_8,"empty runnable").
synonym(v_0,v).
synonym(v_1,v_a).
synonym(v_10,v_x_a).
synonym(v_11,v_x_b).
synonym(v_12,v_x_c).
synonym(v_2,v_d).
synonym(v_3,v_b).
synonym(v_5,v_b_a).
synonym(v_6,v_b_b).
synonym(v_7,v_c).
synonym(v_9,v_x).
text(v_4,nil).
text(v_8,nil).
```

and the `fb2pl.grasem` file is
```
FB2PL {
 facts = ws* fact+
 fact = relation subject object ws*
 relation = qualident ws*
 subject = qualident ws*
 object = color | idobj | strobj | intobj | nothing
 idobj = qualident ws*
 strobj = string ws*
 intobj = number ws*
 color = kwcolor ws*
 nothing = kwnil ws*
 
       /* low-level */
      kwcolor = rgba | "green" | "yellow" | "red"

      keyword = kwcolor | kwnil
      
      kwnil = "nil"

      flat_ident = ~keyword flat_ident_char+ 
      flat_ident_char = ("a" .. "z") | "_" | dig
      qualident = qualident_recursive | flat_ident
      qualident_recursive = flat_ident "/" qualident

      number = dig+
      dig = "0" .. "9"
      rgba = hex hex hex hex
      hex = hd hd
      hd = dig | "A" .. "F"

      string = dq notDQ* dq
      dq = "\""
      notDQ = ~dq any
      ws = " " | "\t" | newline
      newline = "\n"

}


 facts [@ws @fs] = [[${fs}]]
 fact [rel sub obj @ws] = [[${rel}(${sub},${obj}).\n]]
 
 relation [qid @ws] = [[${qid}]]
 subject  [qid @ws] = [[${qid}]]
 object [item] = [[${item}]]
 idobj [x @ws] = [[${x}]]
 strobj [x @ws] = [[${x}]]
 intobj [x @ws] = [[${x}]]
 color [x @ws] = [[${x}]]
 nothing[x @ws]  = [[${x}]]
 

keyword [kw] = [[${kw}]]
kwnil [kw] = [[${kw}]]
kwcolor [kw] = [["${kw}"]]

      flat_ident [@cs] = [[${cs}]]
      flat_ident_char [c] = [[${c}]]
      qualident [ident] = [[${editSlashes (ident)}]]
      qualident_recursive [flatident slash recursiveident] = [[${flatident}${slash}${recursiveident}]]

      number [num] = [[${num}]]
      dig [digit] = [[${digit}]]
      rgba [h1 h2 h3 h4] = [[${h1}${h2}${h3}${h4}]]
      hex [h1 h2] = [[${h1}${h2}]]
      hd [c] = [[${c}]]
 
      string [q1 @cs q2] = [[${q1}${cs}${q2}]]
      dq [c] = [[${c}]]
      notDQ [c] = [[${c}]]

      ws [c] = [[${c}]]
      newline [c] = [[${c}]]
```

# Step 6 Optimization?
The script takes 13 seconds to run on a 2017 MacBook

If we were to proceed from here, maybe we might optimize parts of the script for faster turn-around.

How to optimize the script: 
- place a `set -x` line at the top of the script
- run the script and watch each step.

Obvious optimizations:
- the current script build the .grasem files 5 times, this could be relegated to a single script that built the .grasem files only once.
 
The `build_grasem.bash` file is:
```
#!/bin/bash
set -e
trap 'catch' ERR
target=$1
catch () {
    echo '*** fatal error in run-block.bash'
    exit 1
}

../../grasem/run.bash md2block.grasem >_.js
cat _.js foreign.js >_md2block.js

../../grasem/run.bash block2brace.grasem >_.js
cat _.js foreign.js >_block2brace.js

../../grasem/run.bash brace2fb.grasem >_.js
cat _.js foreign.js >_brace2fb.js

../../grasem/run.bash fb2pl.grasem >_.js
cat _.js foreign.js >_fb2pl.js
```

This has dropped runtime from 13s to 8.7 seconds. 

If we were desparate for faster speed, we could look at improving parsing, e.g. by using `this.primitiveValue` instead of parsing single characters (See Ohm-JS documentation).

Another aspect to be measured is whether the use of temporary files, instead of pipes, is affecting performance.
## Optimization is Not Necessary
Note that optimization is not necessary.

We will run this program very few times, e.g. only during the Architecture phase of the project.

The only reason to optimize this program is to enhance turn-around speed for the Architect.

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
