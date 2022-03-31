---
layout: post
title:  "Bloatware Reduction via File Descriptors"
---
## Bloatware Reduction via File Descriptors

Original problem
1. write to a file, or, 
2. write to console

Bloatware solution (psuedo-code):
```
if (output === 'file') {
    file.write (...)
} else if (output === 'console') {
    console.log (...)
}
```

## Bloatware Reduction

Invent `file descriptors` and let underlying machinery figure out what to do:

```
fd.write (...)
```


## See Also

[Table of Contents](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)
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