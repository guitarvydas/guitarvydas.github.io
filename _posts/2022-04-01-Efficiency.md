---
layout: post
title:  "Efficiency"
---
## Efficiency
Option 1:

```
if (output === 'file') {
    file.write (...)
} else if (output === 'console') {
    console.log (...)
}
```

Option 2:

```
fd.write (...)
```

Option 2 will be more efficient than option 1, regardless of whether you implement the code in a language like `Rust` or `C++`

## See Also

[Bloatware Reduction Case Study](https://guitarvydas.github.io/2022/03/31/Bloatware-Reduction-via-File-Descriptors.html)

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