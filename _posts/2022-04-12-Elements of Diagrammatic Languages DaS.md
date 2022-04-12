---
layout: post
title:  "DaS - Elements of Diagrammatic Languages (WP1)"
---

Thoughts April 12, 2022 ...

## Boxes

### 1Box

![1 Box](/assets/daswp1-1box.png)

### 2Box
![2 Box](/assets/daswp1-2box.png)

### NBox

![N Box](/assets/daswp1-nbox.png)

### 0Box

![0 Box](/assets/daswp1-0box.png)

### Concentric Boxes

### Independent Boxes

## Ports

### Input Ports

![Input Ports](/assets/daswp1-inputport.png)


### Output Ports

![Output Ports](/assets/daswp1-outputport.png)

## Connectors

### Message Connectors

![Asynchronous Connectors](/assets/daswp1-connectors.png)

### Same-Page Connectors

## Text Phrase

### Example Phrases
- ⟪WhenAll⟫
  | when all PredicateBox
- ⟪When⟫
  | when messages
- ⟪Return⟫
  | -> [1]
- ⟪CheckReturn⟫
  | check return [String]
- ⟪FindConnectionFromMe⟫
  | find [1] from me on port [2]
- ⟪Cond⟫
  | cond 【CondClause】【...】
- ⟪WithLock⟫
  | lock [1]
- ⟪Find⟫
  | find [1] in [2] given [ParameterList] => [3]
  | find [1] in [2] => [3]
⟪VarBox⟫
  | var [1] <= $i { { [[2]] } [3] }
  | var [1] <= $o { { [[2]] } [3] }
  | var [1] <=      { [[2]] }
⟪Synonym⟫
  | synonym [1] = { [2]List }
  | synonym [1] = [2]
⟪Lookup⟫
  | lookup [2] => [1]
⟪ForEvery⟫
  = for every item in [1] given [ParameterList] => [2]
  | for every [1] in [1] given [ParameterList] => [2]
  | for every item in [1]  => [2]
  | for every [1] in [1]  => [2]
⟪SynchronousCall⟫
  // no nesting here - Call is a Leaf, not a nested box
  | @ [1] <= [2]
  | @ [1]
  | # [1] <= [2]
  | # [1]


DD
- ⟪Field Accessor⟫ name "." name
- ⟪MethodCallSynchronous⟫ name "(" ... ")" where "..." is a list of DDs

Sub-phrases
- ⟪Predicate⟫【1】where 1 is a Predicate Phrase
- ⟪Datum⟫ [digit] where [digit] is a placeholder for a DD
- ⟪name⟫ [id] where id is a string of characters (alnum)
- ⟪CondClause⟫
  |【Predicate】【1】

Comment

- notes
  - spaces ignored at top level
  - [spaces allowed inside brackets(?)]

#### Example Mapping Phrases -> Operation

  | find [1] in [2] given [ParameterList] => [3]

--> me.findInGiven ([1], [2], [ParameterList], [3])

### String

"abc"

### Name

alnum

### Comment

// to end of line

/* block comment */

## Data Descriptors

[see for basics, ideas](https://guitarvydas.github.io/2022/03/26/Data-Descriptors.html)

## Construction Language

### Methods



### Predicates

### Procedures

### Handlers

`λ₂ (self, message) -> nothing`

Handlers can invoke `Send ()` to create messages which are routed by the handlers' Containers.

### Data Descriptors

## Synonyms

`synonym` *name* `= [1]`

## Example

![Code for Routing](/assets/routing.png)


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
