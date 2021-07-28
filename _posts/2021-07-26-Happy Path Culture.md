---
layout: post
title:  "Happy Path Culture"
---
# Happy Path Culture

Programming suffers from *happy path culture* - a form of chauvanism that denies that design errors can happen.

It is *assumed* that a program will work.

The fact that most software doesn't work until it leaves the development phase, has been largely ignored.

Many languages and tools are based on this happy path assumption, hence, emphasis has been placed on editing baubles (like auto-completion) and strong typing. 

Early languages, esp. Lisp, emphasized debugging and what happens on paths other than the happy path.



# UX Psychology - If It Does Everything, It Must Be Good, Right?

"Correct" programs might not correctly satisfy requirements.

Strong typing helps only with creating programs that satisfy the programmer's idea of what the requirements are.

Strong typing can help with *brainstorming* the requirements, but only does so in an ad-hoc manner.

Maybe, we will never be able to formalize requirements, since requirements are given by humans and only a subset of those are Architects, Engineers and Implementors.

Agile and UML are attempts at formalizing the process of gathering and specifying requirements.

## The Universe vs. The Drunkard's Walk

It might be possible to define the *universe* of possible programming actions and languages.

This, though, is not the same as defining *useful subets* of the universe.

The goal of Designing solutions is to *choose* paths through the universe that make it easier to think about and express Architectures.

DI - Design Intent - is what successful Architects express.

Engineers ensure that all of the T's are crossed and I's dotted in an architecture.

Implementors create code from Engineering specifications.

The goal of the above activities it not to discard details, but to elide them and layer them so that the Design is understandable. [_Designs for practical solutions are rarely easy-to-understand.  Certain practices make them harder to comprehend while other practices make Designs easier to comprehend_.]

## Implementation Languages

Many of the current-day languages are targetted at implementation (Rust, Python, JS, Java, C, etc., etc. (if a language includes a `+` or allows definition of data structures, then it is an implementation language.))

## Languages For DI

I list some of the necessary features for languages that cater to Design Intent:

- Low friction for creating Architectures.
- Low friction for abandoning code and rewriting it when design changes are recognized.
- Low friction to design iteration
- Isolation (build-and-forget).


# See Also

[Isolation II](https://guitarvydas.github.io/2021/06/06/Isolation-II.html)

[Isolation III](https://guitarvydas.github.io/2021/06/07/Isolation-III.html)

[Isolation](https://guitarvydas.github.io/2020/12/09/Isolation.html)

[Blog](https://guitarvydas.github.io)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
