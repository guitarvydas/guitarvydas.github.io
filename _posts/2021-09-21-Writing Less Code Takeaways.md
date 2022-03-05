---
layout: post
title:  "Writing Less Code Takeaways"
---

## APL

The shortest - in lines of code - significant program that I wrote was in APL.

That version of APL had a single purpose - manipulating matrices.

I wrote 2 lines of code and wrote about 80 lines of comments.

Clearly, I felt that the code was write-only and that English comments were needed to make the code and architecture readable by other programmers.

## Terseness

A goal of architecting languages is to write very little code and to spend most of the time thinking about and solving the problem at hand.

There is a saw-off point where the code becomes so terse as to be write-only in nature.

In the APL code I wrote, every character, in the lines of code, performed significantly large operations.

understandability

## Flexibility

Ideally, a system can be architected with so few lines of code that the designer/programmer has no compunction about throwing all of the code away and starting afresh when new architectural discoveries are made about the problem space.

Alternatively, the code written must be so flexible as to allow rearranging of the architecture with little effort.  

Most GPLs discourage this kind of flexibility while encouraging expression of details (which leads to inflexibility[^1]).

[^1]: For example, flexibility requires that no functions be called directly by name - all functions should be called through indirection (DLLs provide a degree of indirection, but discourage full flexibility by retaining function names).

## Writing Less Code

- Lisp is one way to write *less* code.
- Diagrams are a way to write *less* code.

# See Also
[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)
[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC9EJr0nKHwadbHUtc5zHdmQ/videos)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
