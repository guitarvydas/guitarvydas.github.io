---
layout: post
title:  "Compiler Pipelines"
---
Compilers can be built in a pipeline.

Each stage in the pipeline is driven by syntax ('pattern matching').

Each stage strips out sugar and adds semantic information the next stage.

PT Pascal was one of the early attempts at building a compiler as a pipeline.

The stages in the pipeline are:

1. Scanner
2. Parser
3. Semantic
4. Coder

## Scanner 
- tokenizes the program text and passes a stream of tokens downstream.

## Parser 
- Parses the incoming token stream and checks that they form legitimate phrases in the programming language being compiled
- strips syntactic sugar from the stream before passing the stream downstream
- aborts the pipeline if the incoming text does not form legitimate phrases.

## Semantic Pass
- creates tables for identifiers
- checks declaration-before-use
- creates tables for function signatures (args)
- check that functions are called with appropriate number of args and types
- reports errors, tries to recover and produce as many meaningful error messages as possible
- aborts pipeline if any errors are found
- augments the token stream with semantic information (e.g. location of variables - (parameters, temps, statics, etc.))

## Coder
- if invoked, it is known that the input token stream represents a valid program
- the Coder converts the incoming token stream into valid assembler opcodes+operands for a specific architecture 
- (see Orthogonal Code Generator follow-on for how retargetting can be generalized)

## Conventions
- S/SL is a dataless language - objects and errors and tokens can only be referred to by handles, but not defined in S/SL (the implementation of objects is done in some underlying language, e.g. Pascal, C, etc.)
- tokens are named with "t" as the first letter of the name
- operations are named with "o" as the first letter of the name
- objects are implemented in single-level Objects, called "mechanisms" (aka Modules)
- objects are usually implemented as stacks (aka, "concatenative languages", aka, "stack machines", aka, "Forth-like", aka mid-1900s version of "De Bruijn indexing")
- operations on objects usually involve the top-of-stack and, maybe, other elements near the tops of stacks

## See Also

[PT Pascal and S/SL](https://research.cs.queensu.ca/home/cordy/pub/downloads/ssl/)

[Names and Data Descriptors](https://guitarvydas.github.io/2022/03/24/Names-and-Data-Descriptors.html)

[Data Descriptors - a compile-time model of data and addressing](https://dl.acm.org/doi/10.1145/24039.24051)
[OCG](https://books.google.ca/books/about/An_Orthogonal_Model_for_Code_Generation.html?id=X0OaMQEACAAJ&redir_esc=y)

[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)
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