---
layout: post
title:  "Refactoring Takeaways - Architecture"
---

## Mars Rover Disaster
The [Mars Rover disaster](https://www.rapitasystems.com/blog/what-really-happened-software-mars-pathfinder-spacecraft) caused the Mars Rover software to behave unexpectedly after the unit landed on Mars.

# Priority Inversion

The mis-behaviour was ostensibly caused by "priority inversion".  

This was seen as a bug in the RTOS (realtime operating system).

From my perspective, the bug was due to the problem of pushing a notation beyond its "comfort zone".

Functional notation is appropriate for reasoning about calculators, i.e. synchronous sets of inputs which always cause synchronous outputs.  The simplicity of this paradigm is lost when it is applied to concurrent processes, as witnessed by the accidental complexity that caused priority inversion.

The bug was later addressed by the addition of more complexity (priority inheritance) which repaired the immediate problem in the notation, but did not address the deeper problem (that of pushing a single notation beyond its boundaries of simplicity).

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
