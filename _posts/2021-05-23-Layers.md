---
layout: post
title:  "Layers"
---

# Asynchronous
  Send() down
  Wait for response(s) from children.
  filter children's responses, then Send() response
## Children
  Children Send() response(s).
  - N.B. Children operate in any order.
  - N.B. Child sequencing determined by Scheduler.
# Synchronous
  loop for all children collecting responses
	Call() down.
	_stall_
    save response.
  end loop
  filter reponses and Return().
## Children
  Children invoke Return to send responses.
  - N.B. Children operate in the order given by the loop.
  - N.B. Child sequencing determined by Parent.
  
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
