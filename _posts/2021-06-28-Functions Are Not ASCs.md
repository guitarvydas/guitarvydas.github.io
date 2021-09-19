---
layout: post
title:  "Functions Are Not ASCs"
---

ASC means Asynchronous Software Component.

Functions are not ASCs.

Functions rely on other - synchronous - functions (and libraries).

The smallest unit of componentization in current PLs[^1] is the _thread_.

_Threads_ typically imply the use of _operating systems_[^4].

It should be possible to implement "better" (smaller, faster) components using _messages_ and _closures_[^2].

The main issue is how to structure message-sending components to avoid spaghetti designs.[^3]

[^1]: PL means Programming Language.
[^2]: Operating system processes - threads - are ad-hoc implementations of closures.
[^3]: The answer to how to create systems of structured components, is, as always, to use hierarchy and scoping.

[^4]: Operating systems are not needed.
# See Also

[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
