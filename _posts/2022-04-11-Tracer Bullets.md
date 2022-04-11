---
layout: post
title:  "Tracer Bullets"
---

When debugging a concurrent app - one with many possible paths of execution - one wants the equivalent of *tracer bullets* to see where messages have gone, and, come-from.

A single backtrace is not enough.

## Implementation

Tracer bullets are straight-forward to implement in Common Lisp and JavaScript.

Tack the previous message onto the end of the current message (recursively, each message contains a trace of messages that caused them).

I'm experimenting with a `Message` class that has two main fields and two trace fields:
1. tag
2. data
3. come-from id
4. previous message.

Since each message is defined as above, `previous message` becomes a nested list from the beginning of time.

Currently, I output traces in Lisp syntax and use a Lisp pretty printer to view them (emacs *indent-region* in my case).

Fields (1) and (2) are *real*.  Fields (3) and (4) are for debugging.


## See Also

[Message Class]()

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
