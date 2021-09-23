---
layout: post
title:  "Compiler Technology Takeaways 2"
---
- normalization

# gcc

The Gnu C compiler uses RTL

RTL was invented as a peepholing technology by Fraser-Davidson.

# OCG
Orthogonal Code Generator (Cordy).

OCG is a declarative decision language for portability.

OCG splits portable code generation into two sub-tasks:
1. Compile the input program to a normalized form.
2. Convert the normalized form to code for specific CPU.

# Denotational Semantics
Denotational Semantics is a functional description of PL[^pl].

[^pl]: PL means Programming Language.
Includes grammar + semantics + code emission.

Denotational Semantics was, originally, an _all-in-one_ concept resulting in large compilers that were not practical.

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

[OCG](https://books.google.ca/books?id=X0OaMQEACAAJ&dq=bibliogroup:%22University+of+Toronto+Computer+Systems+Research+Institute+Technical+Report+CSRI%22&hl=en&sa=X&ved=2ahUKEwig1Legm8bqAhWvlHIEHYzzBYEQ6AEwBHoECAEQAQs)

[RTL](https://www.researchgate.net/publication/220404697_The_Design_and_Application_of_a_Retargetable_Peephole_Optimizer)

[Data Descriptors](https://dl.acm.org/doi/abs/10.1145/24039.24051)

[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html)



<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
