---
layout: post
title:  "Isolation IV"
---

Call / Return breaks isolation, because it makes ad-hoc scheduling decisions.

Call makes a scheduling decision:
- Call implies that the caller will suspend immediately.
- Call implies that the callee is immediately scheduled to run and runs immediately.
- Call implies that the caller executes a WAIT (for the callee).

Return is a scheduling decision.
- The callee dies and immediately resumes the caller.

Operating systems deal with such ad-hoc scheduling decisions using a sledge-hammer called _preemption_.

Call/Return is baked into the hardware of modern CPUs.  This was not always the case.  Even _stacks_ were not automatically-managed in earlier CPUs.

# See Also

[Blog](https://guitarvydas.github.io)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
