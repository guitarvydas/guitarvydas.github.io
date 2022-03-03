---
layout: post

title: "Optimizing"

---
RTL (Register Transfer Logic) was used by GCC.

RTL was written up in a paper by Fraser-Davidson ("... Peephole optimizer ..." - see References).

RTL works by treating *everything* as a register, then optimizing certain runs of register logic into better (faster) code.

I used *awk* to build a peephole optimizer for my 8080 C compiler.

The algorithm for peepholing is trivial - (1) search for a pattern, then, (2) replace (even Word® can do this :-).

How do you search for a pattern?  Brute force.  Also known as inferencing / backtracking / PROLOG / miniKanren / core.logic / Relational Programming.

How do you replace?  At the character-level (e.g. REGEX), *sed* does the trick.  If you search/replace trees then you need a tree rewriter (aka Lisp).

What else does search?  

Parsers.

What does inferencing search+replace?  PEG, Ohm-JS, TXL.ca.

[aside: I built an OCG - Cordy's Orthogonal Code Generator.  OCG is a declarative spec of a code rewriter.  See References, again.]

[aside: Cordy used "condition descriptors" which bear a striking resemblance to Church 1 and 0 - true and false.]

To do recursive exhaustive search, you want something that does recursive inferencing (e.g. Relational programming, PROLOG, Ohm-JS, etc., etc.).

# PROLOG Simplified

See Holm's Prolog Control in 6 Slides.

## On Optimizing BLC

It should be possible to write a peephole optimizer for BLC (say, in awk, or JS, or perl, or Python, or ...) that finds certain runs of lambdas and replaces them by other code, more tuned to the target CPU architecture.

To optimize code for speed, you need to de-optimize for size (and scalability).

This could be done by The Loader.  (Currently, this is done, in an ad-hoc manner, by The Compiler).

# See Also
[References](https://guitarvydas.github.io/2021/01/14/References.html)
[BLC](https://justine.lol/lambda/)
[Prolog Control in 6 Slides](https://www.t3x.org/bits/prolog6.html)
[Ohm in Small Steps (Scheme to JS experiment)](https://computingsimplicity.neocities.org/blogs/OhmInSmallSteps.pdf)
[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
