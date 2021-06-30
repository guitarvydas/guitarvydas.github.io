---
layout: post
title:  "Status"
---
Projects On The Go as of June 29, 2021:

# ASC
- Asynchronous Software Components
- currently working on relative naming objects
- github: https://github.com/guitarvydas/asc-manually/tree/master/v2

##	done: SCN (mini-DSL) for writing ASCs
### identity.bash
consumes xxx.asc and emits same (identity)

### lisp.bash
consumes xxx.asc and emits Lisp

### rid-dsl
- mockup of SCN for RID expander
- RID means relative-id
- SCN means Solution-Centric Language, e.g. a mini-DSL

# TYPE SCN
- github: https://github.com/guitarvydas/asc-manually/tree/master/v2/types
- SCN (mini-DSL) for minimal set of types for writing ASC engine
- on the order of 6 operations
- maybe will become a semantics-combinator, akin to existing parsing-combinators

## tyengine.lisp
spec for TYPE SCN

## asctypes.ty
- definition of types using TYPE SCN
- intended as type system for ASC engine

# SEML
- SCN (mini-DSL) for semantics portion of Ohm-JS
- IDE for developing semantics code when grammar already works (Ohm-JS)
- will use knowledge from GLUE and GRASEM (see below)

# mkglue.py
# Hello World ASC
- convert drawings to `.md` (manually) as demonstration of basic ideas

# Essays
- https://guitarvydas.github.io

# Other Projects
## Arithmetic

### GLUE
### GRASEM
### ArrowGrams
- full diagram-to-code transpiler (lisp + Haskell + prolog-ish)

- github: https://github.com/bmfbp/bmfbp (see svg/... and build_process/...)

- probably could be re-expressed more cleanly using ASCs

  

### JS-PROLOG

### AG-JS

### CL-EVENT-PROCESSING
### PASM 

- parser assembler-like primitives
- probably similar to parser combinators

### Scanner

- tokenizer pipeline
- like scanner combinators, but fixed pipeline
- tokenizer | comments | strings |  spaces | symbols | integers
- github: https://github.com/guitarvydas/scanner 
- see: README.org

### SL

### ESA + ESA-TRANSPILER

### ASON

### CL-HOLM

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
