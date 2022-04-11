---
layout: post
title:  "UX - Parameter Counting - Gradual Compiling"
---

In JavaScript, I wrote `f(x,y,name,z)`

but intended to write `f(x,y.name,z)`

A long debugging session was required to discover that `z` was `undefined`.

I gave 4 params, but `f` expected only 3.

The 4th parameter *defaulted* to `undefined`.

A simple compiler-check (count parameters), would have caught this typo.  Instead it caused a mystery.

## Why?

I would guess that parameter defaulting was inserted into the language in-search-for user-friendliness.

## Conclusion

### User Friendliness

This is not user friendly.

### Simple Checks

Full-blown type-checking would not have been necessary here.  

Just parameter-counting.

#### Re-Structuring Semantics Checking?

Hmm, we use a *parser* to check for stupid errors.  

We don't waste time waiting for a full type-check, if the parser caught stupid errors.

Maybe a pre-check pass should be inserted between the parser and the full-blown semantics checker?

How does this affect language design and user-friendliness?  And, gradual typing?

#### Gradual Compilation

Maybe languages shoud be structured to allow experimentation, then, whine about "not enough information (detail) to compile" later?

![Gradual Compiling](/assets/gradualcompiling.png)

## See Also

[Table of Contents as of Dec. 01 2021](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)
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
