---
layout: post
title:  "Type Descriptors (Working Paper)"
---

A Type Descriptor has two fields:
1. collection
2. base type.

# Collection
The collection field can have one of 3 values:
1. _collection name_
2. "\_any\_"
3. "".

Examples (respectively):
```
namespace [name]
[name]
name
```
where "name" is a user-defined type, and "namespace" is a user-defined collection type.

The form `[name]` uses the builtin collection type and allows any type(s) in the collection (like Lisp lists).

# Base Type
The Base Type is the name of some other type.

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
