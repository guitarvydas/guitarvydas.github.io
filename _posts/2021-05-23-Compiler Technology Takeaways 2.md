---
layout: post
title:  "Compiler Technology Takeaways 2"
---
- normalization

# gcc

The Gnu C compiler uses RTL invented as a peepholing technology by Fraser-Davidson.

# OCG
Orthogonal Code Generator (Cordy).

Declarative decision language for portability.

Splits portable code generation into two sub-tasks:
1. Compile input program to normalized form.
2. Convert normalized form to code for specific CPU.

# Denotational Semantics
Functional description of PL[^pl].

[^pl]: PL means Programming Language.
Includes grammar + semantics + code emission.

Originally an _all-in-one_ concept resulting in large compilers that were not practical.

Peter Lee "Realistic Compiler Generation" broke the concept down into sub-tasks and produced more practical results.
# Normalization
- Triples
- Data Descriptors
## Opcodes
Opcodes are triples.
```
MOV R0,R1
```
## RTL
Register Transfer Logic created by Fraser/Davidson as peephole technology for portability.

Splits code selectiion into two sub-tasks
1. Compile input program to normalized form (RTL "everything is a register")
2. Convert normalized form to code for specific CPU.
## Data Descriptors
Normalized form for description of data locations.

Enables splitting of portable compilers into smaller sub-tasks.
# See Also

https://guitarvydas.github.io/2021/01/14/References.html
https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html


<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
