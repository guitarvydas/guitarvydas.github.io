---
layout: post
title:  "Interpreters"
---

The earliest interpreters read the program in line-by-line and interpreted each line as they were read in.

GOTO was a "problem". It meant that the interpreter had to re-read certain lines and had to re-interpret those lines.

Quickly, it was realized that interpreters could be made more efficient.

First, interpreters just read all of the lines into memory, in a buffer.

Then, interpreters started to use "bytecodes", but every interpreter used a different set of bytecodes. (The first one I remember seeing was Tiny Basic (https://en.wikipedia.org/wiki/Tiny_BASIC)).

Then, they noticed that EVERY interpreter used a different set of bytecodes.

This was "standardized" and became a VM. I *think* that the first VM was in early Smalltalk (https://en.wikipedia.org/wiki/Virtual_machine), but Java really popularized the concept with the JVM. Sun produced Java and backed/advertised the JVM.

# See Also

[Blog](https://guitarvydas.github.io)
[Table of Contents as of Sept 17, 2021](https://guitarvydas.github.io/2021/09/21/Table-of-Contents-Sept-17-2021.html)
[Videos](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy5)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
