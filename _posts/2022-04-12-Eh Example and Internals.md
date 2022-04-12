---
layout: post
title:  "ė (eh) Example and Internals"
---

I describe the implementation of a very simplistic example using inner concurrency and a handful of diagrams.

The example is `cat`.  It copies the contents of a file to the console character by character.  It, also, outputs each character on a port (currently unused).

## Top Level

![Top Level of The Simple Example (cat)](/assets/cat![[cat.png]].png)

(obsidian:
![cat.png](file:///Users/tarvydas/Desktop/blogs/guitarvydas.github.io/assets/cat.png)
)

The diagram represents a very simple system with three (3) components total
- a Container
- two (2) Leaf components.

The Container is called `top`.

The Leaf components are called `read` and `write`.

`Top` runs the two leaves concurrently and routes messages between them.

`Top` is called (invoked) like a normal function and can return values like a normal function.  (In this example, `Top` doesn't bother to return anything).

When `Top` is invoked, it is passed two (2) parameters
1. the filename to be read
2. the filename to be written (which is ignored in this simple example, this example simply prints characters on the console and doesn't write them to a file).

## See Also

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
