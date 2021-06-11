---
layout: post
title:  "Hierarchical Namespaces"
---

All names shall be extracted from namespaces.

(This means that not only variable names, but function and type names be placed in namespaces).

Namespaces shall be hierarchical.

Namespaces can contain namespaces.

A fully qualified name consists of 3 parts[^3parts]:
1 component
2 namespace within the component, i.e. i/o/x/c/n (input, output, connection, component, other names, resp.)
3 name (a string or a symbol).

Corrollary: Each _software component_ contains 5 namespaces. Names are unique within a namespace, but may duplicate names in other namespaces, e.g. a _software component_ might contain an input called "a" and an output called "a" without any name-clashing problems (the first "a" is in the input namespace, whereas the second "a" is in the output namespace).

A name can be represented by a tuple `{component, namespace, name}`.

Names are relative and nested, in general, the above tuple is recursive, e.g.
`\{\{component, namespace, name} namespace name}`.

The namespace syntax is not meant to be easily human-readable.

Purely for human readability, we abbreviate namespace notation in UNIX-like syntax:

`./c/outer/i/name`

where '.' means the root component (also known as "self") and the namespaces are abbreviated to a single letter `i/o/x/c/n`.

[^3parts]: The fact that fully qualified names have 3 parts is not to be confused with the use of triples. Triples are a more general construct.
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
