---
layout: post
title:  "PT Notes for Torlisp - Language Jam"
---
# Language Jam (langjam)
### Theme
First Class Comments
### Restrictions
48 hours to implement and document
### My Approach
#### Goal
Executable diagrams
#### README.md
[README.md](https://github.com/langjam/jam0001/blob/main/guitarvydas/README.md)
#### Sequence Diagram

#### Tools
- Ohm-JS
- SWIPL (PROLOG
- /bin/bash commands: cat, tsort, mv, sed, (and scripts)
#### 2 Kinds of Diagrams
1. *Sequence diagram* (Pert Chart) (boxes joined by arrows denoting ordering)
2. *Details diagram* (snippets of /bin/bash code in red boxes)

#### Sequence Diagram

<img src="https://raw.githubusercontent.com/guitarvydas/jam0001/guitarvydas/guitarvydas/sequence.png" alt="img" style="zoom:67%;" />

#### Details Diagram

<img src="https://raw.githubusercontent.com/guitarvydas/jam0001/guitarvydas/guitarvydas/details.png" alt="img" style="zoom:67%;" />

#### Sequence Transpiler

5 Ohm-JS passes -> sort -> PROLOG -> JSON -> Ohm-JS to /bin/bash

#### Details Transpiler

6 Ohm-JS passes -> sort -> PROLOG -> JSON -> Ohm-JS to /bin/bash

##### Passes

Each pass consists of 2 specifications:

1. grammar (*.ohm)
2. action code (aka _semantics_) (*.glue)

Each pass *augments* the factbase (fb.pl), there is no need to remove[^1] facts.

[^1]: Removing facts is an optimization that is not needed on current hardware.  Diagrams remain small, so runtime is imperceptable. Keeping facts allows for future flexibility (e.g. querying the fact base and making inferences that were not foreseen during original development).

##### Sequence Transpiler Passes

1. compressed .drawio file -> uncompressed .XML
2. normalize attributes (e.g. style="...") 
3. cull attributes, discard attributes that are concerned only with graphical representation (keep: value, source, target, edge, vertex, id, green, yellow, red)
4. symbol table - map long id names to short id names (not strictly necessary, but aids human readability duing bootstrap)
5. culled .XML -> factbase (fb.pl)
6. sort - needed only to appease PROLOG (original PROLOG required that all clauses be grouped together, while modern PROLOG relaxes this constraint.  The _sort_ pass appeases original PROLOG.)

##### Details Transpiler Passes

1. compressed .drawio file -> uncompressed .XML
2. normalize attributes (e.g. style="...") 
3. cull attributes, discard attributes that are concerned only with graphical representation (keep: value, source, target, edge, vertex, id, green, yellow, red)
4. symbol table - map long id names to short id names (not strictly necessary, but aids human readability duing bootstrap)
5. culled .XML -> factbase (fb.pl)
6. fold newlines, create one newline-less string for each snippet of code (helps sort)
7. sort - needed only to appease PROLOG (original PROLOG required that all clauses be grouped together, while modern PROLOG relaxes this constraint.  The _sort_ pass appeases original PROLOG.)

##### Sequence JSON

```
{"diagram":"id1", "toplevelcomponent":"id4"}

{
  "children": ["process A", "process B" ],
  "connections": [
    {
      "name":"x2",
      "source": {"component":"process A", "port":"fb"},
      "target": {"component":"process B", "port":"in"}
    }
  ],
  "diagram":"id1",
  "id":"id4",
  "inputs": [],
  "name":"topLevel",
  "outputs": [],
  "synccode":""
}
{
  "children": [],
  "connections": [],
  "diagram":"id1",
  "id":"id5",
  "inputs": [],
  "name":"process A",
  "outputs": ["fb" ],
  "synccode":""
}
{
  "children": [],
  "connections": [],
  "diagram":"id1",
  "id":"id6",
  "inputs": ["in" ],
  "name":"process B",
  "outputs": [],
  "synccode":""
}


```

##### Details JSON

```
{"diagram":"id1", "toplevelcomponent":"id4"}

{
  "children": ["process A", "process__B" ],
  "connections": [],
  "diagram":"id1",
  "id":"id4",
  "inputs": [],
  "name":"top level",
  "outputs": [],
  "synccode":""
}
{
  "children": ["code1" ],
  "connections": [],
  "diagram":"id1",
  "id":"id5",
  "inputs": [],
  "name":"process A",
  "outputs": [],
  "synccode":""
}
{
  "children": [],
  "connections": [],
  "diagram":"id1",
  "id":"id6",
  "inputs": [],
  "name":"code1",
  "outputs": [],
  "synccode":"@~@echo hello@~@echo ... from process A@~@"
}
{
  "children": ["code2" ],
  "connections": [],
  "diagram":"id1",
  "id":"id7",
  "inputs": [],
  "name":"process__B",
  "outputs": [],
  "synccode":""
}
{
  "children": [],
  "connections": [],
  "diagram":"id1",
  "id":"id8",
  "inputs": [],
  "name":"code2",
  "outputs": [],
  "synccode":"@~@echo ... from process B@~@echo goodbye@~@"
}

```



### Relationship to Lisp

- PEG parsing <- generalization of Lisp macros
- PEG parsing in a separate pre-pass accomplishes the same result as hygenic macros, except with less complication (YMMV)
### Fallout

- created _ftranspile()_ and _stranpsile()_ functions to abstract (hide) transpiler functionality

### Continuing Work

- "eat your own dogfood" - compiled diagram of diagram compiler
- simplification of code

 [firstclasscomments](https://github.com/guitarvydas/firstclasscomments)

### Github
[lamgjam](https://github.com/langjam)
### Winners
[Winners](https://youtu.be/j7VAw8UfMeA)
# PEG for Zodetrip

# See Also

[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy5)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
