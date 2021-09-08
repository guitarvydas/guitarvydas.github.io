---
layout: post
title:  "PT Notes for Torlisp - PEG for Zodetrip"
---

# Goal

Use "#lang peg" to convert portions of Zodetrip.rkt.

[_Zodetrip was discussed in an earlier Torlisp meeting.  Zodetrip is a game jam entry written in racket, by Jos'h Fulller_]

# Progress

Small amounts of progress, not finished yet.

- Step 1: (done) chop zodetrip.rkt into separate files (modules)

- currently trying to determine is knowledge of racket macros will be necessary

- Step 2: (in progress) convert keying function to "#lang peg" (requires knowledge of how to emit _case_ from _peg_)

- fallout:

  ​		[keying rough-in slides](https://guitarvydas.github.io/2021/09/07/Keying-For-Zodetrip.html)

  1. [racket macros slides (unhygenic vs hygenic example)](https://guitarvydas.github.io/2021/09/07/Racket-Macros.html)

# Github

[zodetrip](https://github.com/guitarvydas/zodetrip-0.9.7-src)



# See Also

[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy5)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
