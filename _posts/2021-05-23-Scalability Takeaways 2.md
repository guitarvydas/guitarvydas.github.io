---
layout: post
title:  "Scalability 2"
---
A scalable component is one which coordinates children components and filters their results.

- input: commands from parent
- output: filtered data to parent
- contains: child components.

Children can _send_ information to parents and commands/requests to their own children.

Children must not leak information in any other direction.

A parent completes an operation when all of its children have completed sub-operations. 

Corollary: a parent component is busy as long as any of its children components are busy (recursively).

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
