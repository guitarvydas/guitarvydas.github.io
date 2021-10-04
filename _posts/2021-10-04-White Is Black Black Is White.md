---
layout: post
title:  "White Is Black, Black Is White"
---
# Interpreters vs. Compilers

*All* languages can be interpreted.

Only *some* languages can be compiled.

Compilation is an optimization, often applied prematurely.

# Concurrency, Asynchronocity

Computers are asynchronous and concurrent.

Pogramming languages, to be useful in orchestrating the actions of computers, must:

1. express concurrency[^1]
2. then, apply tactics - such as dropping into the synchronous paradigm - to code.

[^1]: Note that *thread libraries* relegate concurrency to second-class status. Most programming languages (such as Python, Bash, etc., etc.) relegate concurrency to second-class status.  A language is first-class concurrent if *every* operation is concurrent by default (function, statement, line of code, etc., etc.).  Special syntax is used only to drop into synchronous code.

# See Also

[Blog](https://guitarvydas.github.io)
[Table of Contents](https://guitarvydas.github.io/2021/09/21/Table-of-Contents-Sept-17-2021.html)
[Videos](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy5)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
