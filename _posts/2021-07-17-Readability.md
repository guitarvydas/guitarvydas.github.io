---
layout: post
title:  "Readability"
---

Programming language Readability is of, at least, two layers:
1. Human Readability
2. Machine Readability.

To date, programming language designers have been emphasizing human readable syntaxes.

To date, we think of programming to consist of only 2 layers:
- machine code (assembler, etc.)
- human-readable PLs.

Machine readable languages enable automatic manipulation of source code.

Machine readable languages enable layering, e.g. allowing more than 2 layers for software designs.

Human-readable languages can be automated using parsers. (REGEXP is a subset of parsing). 

The belief that only 2 layers are possible, leads to:
- the belief that PLs can be designed and implemented by only a select few (interpreter and compiler people)
- the belief that PL technology is split into only 2 parts - compile-time and run-time
- mixing implementation details with DI (Architectural) details
- an uneven blend of DI vs. Implementation details in a language (depends on the language designer). For example, data abstraction is a DI concern, whereas low-level operations, like "+", are implementation details.[^user]

[^user]: Note that user-defined data structures are actually Implementation details.


# Human Readable
Basically, any language that "has syntax" is meant for human consumption.

Syntax is a way to error-check programs written by humans.

Examples:
- Pascal
- Python
- HTML
- spreadsheets

# Machine Readable
Examples:
- assembler
- bash, *sh
- CL (Common Lisp)
- JS (JS is schizophrenic - it contains syntax, but also contains machine-level concepts)

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
