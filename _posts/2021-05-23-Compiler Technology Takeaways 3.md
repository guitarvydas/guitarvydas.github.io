---
layout: post
title:  "Compiler Technology Takeaways 3"
---
- optimization
- portability


# Optimization

Make a program boring.

Someone else will, later, optimize it under-the-hood.

# Portability

Forget about addressing portability directly.

Portabilty is a subset of optimization.

Normalize the program.  Optimization techniques can be used to port the program to other architectures.

RTL ports programs to disparate CPU architectures using normalization ("everything is a register").

OCG ports programs to disparate CPU architectures using normalization ("everything is a lower-level operation using Data Descriptors").

OCG provides a declarative syntax for describing portability decision trees.

Portability is a subset of Projectional Editing.  Projectional Editing is a subset of Normalization.

# See Also

[OCG](https://books.google.ca/books?id=X0OaMQEACAAJ&dq=bibliogroup:%22University+of+Toronto+Computer+Systems+Research+Institute+Technical+Report+CSRI%22&hl=en&sa=X&ved=2ahUKEwig1Legm8bqAhWvlHIEHYzzBYEQ6AEwBHoECAEQAQs)

[RLTL](https://www.researchgate.net/publication/220404697_The_Design_and_Application_of_a_Retargetable_Peephole_Optimizer)

[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
