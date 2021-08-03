---
layout: post
title:  "Flipping Code"
---

We show how to flip large chunks of text in a transpiler, using a small change in the code.

# Desired Output
## Input
We're working a code markdown to bash converter.

At this point, the input looks like:
```
# _containment_

## _fb pipeline_
	allContains1
	printAllDeepContains
	printAllDirectContains



## _details_
### allContains1
	load fb
	load onSameDiagram
	load contain1
### printAllDeepContains
	load fb
	load onSameDiagram
	load contains2
### printAllDirectContains
	load fb
	load onSameDiagram
	load contains3
```
## Desired

The lines in the `_fb pipeline_` are meant to be *bash* and the `###` chunks are meant to be *bash* functions.

*Bash* requires declaration before use, so, at this stage, we want the `fb pipeline` lines to come *last*.

For example, we want and intermediate result of:
```
# _containment_



## _details_
### allContains1
	load fb
	load onSameDiagram
	load contain1
### printAllDeepContains
	load fb
	load onSameDiagram
	load contains2
### printAllDirectContains
	load fb
	load onSameDiagram
	load contains3


## _fb pipeline_
	allContains1
	printAllDeepContains
	printAllDirectContains

```

This can be done with a minor tweak in the *emit* code...

# Grok
```
Pseudo {
  Main = "{" id Commands Details "}"
  Commands = "{" id Block+ "}"
  Details = "{" id Block+ "}"
  Block =   "{" id (id | Block)+ "}" -- rec
          | id+           -- flat

  id = italicid | ident
  underscore = "_"
  newline = "\n"
  spc = " "
  notEOL = ~newline any
  italicid = underscore ident underscore
  ident = firstChar followChar*
  firstChar = letter
  followChar = alnum | " "
}
```
# Emit
```
Main [lb id commands details rb] = [[# ${id}\n${commands}\n${details}]]
Commands [lb id @choices rb] = [[# ${id}\n${choices}]]
Details [lb id @choices rb] = [[# ${id}${choices}]]
Block_rec [lb id @b rb] = [[${lb}${id}${b}${rb}]]
Block_flat [@ids] = [[${ids}]]

id [name] = [[${name}\n]]
underscore [c] = [[${c}]]
newline [c] = [[${c}]]
spc [c] = [[${c}]]
notEOL [c] = [[${c}]]
italicid [u1 id u2] = [[${u1}${id}${u2}]]
ident [f @cs] = [[${f}${cs}]] 
firstChar [c] = [[${c}]]
followChar [c] = [[${c}]]
```
# The Flip
Change 1 line:
```
Main [lb id commands details rb] = [[# ${id}\n${commands}\n${details}]]
```
to
```
Main [lb id commands details rb] = [[# ${id}\n${details}\n${commands}]]
```

## Github
[The Flip](https://github.com/guitarvydas/md2bash/tree/flip)


# See Also

[Blog](https://guitarvydas.github.io)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
