---
layout: post
title:  "The Bare Essence"
---

The bare essence of successful component-based software is:
1. concurrency
2. isolation.

# Concurrency

Concurrency is often conflated with parallelism.

Concurrency is a paradigm.

Parallelism is just a problem-to-be-solved.

All parallel programs are concurrent.

Not all concurrent programs are parallel.

I found that [Rob Pike's talk](https://www.youtube.com/watch?v=oV9rvDllKEg) gave me words to describe this split (concurrency vs. parallelism).

# Isolation

We want [isolation](https://guitarvydas.github.io/2020/12/09/Isolation.html).

# Synchronous Language Plus a Thread Library 

A synchronous language plus a thread library is _not_ the same as starting out with an asynchronous language.

The thought patterns are quite different.

I have never seen a successful drawing language which started out life synchronously, nor have I ever seen LEGO-like snap-together blocks done with synchronous thinking.  (API's don't even come close).

# See Also

[Isolation II](https://guitarvydas.github.io/2021/06/06/Isolation-II.html)
[Isolation III](https://guitarvydas.github.io/2021/06/07/Isolation-III.html)
[Isolation IV](https://guitarvydas.github.io/2021/08/16/Isolation IV.html)
[Asynchronous Thinking](https://guitarvydas.github.io/2021/07/06/Asynchronous-Thinking.html)

[Blog](https://guitarvydas.github.io)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
