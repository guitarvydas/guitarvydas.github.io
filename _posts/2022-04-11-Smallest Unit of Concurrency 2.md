---
layout: post
title:  "Smallest Unit of Concurrency 2"
---

smallest unit of concurrency that I can think of, with more detail:

```
wrapper {
    var mutable flag
    CALL λ₁
    CLR flag
loop:
    TEST flag
    BRNZ exit
    CALL λ₂
    BR loop
exit:
    CALL λ₃
}
```
```
λ₁ - begin
λ₂ - message handler
λ₃ - finish
```
```
λ₁ (self, &rest args)
λ₂ (self, message)
λ₃ (self)
```

## See Also
[Smallest Unit of Concurrency]()

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
