---
layout: post
title:  "On Designing a DSL"
---
Re: "Designing a DSL for accounting:..." (see appendix).

The article shows how to build a “project plan” for creating a new DSL.

I think that that is too formal and propagates the notion that DSLs are difficult to build.

Yet, many people build and use DSLs without realizing it.  For example, by using REGEXP.

REGEXP is a DSL.

Regular expressions are often used to specify patterns that make up other (usually trivial) DSLs.

Programmers do not create project plans for using REGEXP.  They just use REGEXP.

At what point do you stop planning and Just Use the thing?

I don’t know, but I see a chasm between: 
1. straight-forward programming to solve a problem (using REGEXPs as one tool, along with other tools)
2. embarking on a mega-project to build apparently woo-woo scary apps like compilers[^1].

[^1]: Compilers are not difficult to build.  They are simply big apps that contain lots of detail.

Currently, PEG falls into the scary realm and REGEXP doesn’t.

I think that PEG should be non-scary, like REGEXP.

The differences between PEG and REGEXP are:

1) PEG needs many lines of code to describe a text-match and transformation

2) PEG is more powerful than REGEXP, because PEG provides subroutines and REGEXP doesn’t.

I think that the ideal situation for programming would be to use an IDE that works like a heads-up display.

One window for the grammar, another for the glue-ing (transforming the matching bits) and various other windows for things like debugging, etc.

When more than one DSL is used for one problem, the heads-up display would contain more windows.

# Batch Edit
Thought: maybe I think of PEG in terms of "batch edit".

# Appendix 
[Designing a DSL for accounting: ...](https://click.convertkit-mail.com/e5u4m3mqx7u0u294r7f8/7qh7h8h4gg5knmbz/aHR0cHM6Ly90b21hc3NldHRpLm1lL2ZpbmFuY2lhbC1hY2NvdW50aW5nLWRzbC8_dXRtX3NvdXJjZT1uZXdzbGV0dGVyJnV0bV9tZWRpdW09ZW1haWwmdXRtX2NhbXBhaWduPW9uYm9hcmRpbmdzZXF1ZW5jZQ==,)

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
