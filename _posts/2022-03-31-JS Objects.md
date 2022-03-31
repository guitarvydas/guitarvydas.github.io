---
layout: post
title:  "JS Objects"
---
## Synopsis
This is my understanding of how JavaScript objects are stored, before optimization.

## Everything Is An Object

Everything is an *object*, including *functions*.

### Except Atomic Things
- code is atomic - it is probably a blob of bytes, maybe a string of source code(?)
- integers are probably atomic
- booleans - true/false - are probably atomic
- strings are atomic - probably a blob of bytes
- the two-slot tuple (struct) that represents objects is probably atomic
- list cells are atomic

- (arrays are made of atomic list cells)
- (continguous arrays of objects can be optimized (to remove CDRs))

## Drawing - Atomic Structures
![atomic objects](/assets/js-object-atomic-structures.png)

## All Objects Have Two Slots

![objects](/assets/js-object-objects.png)

### Prototype Is A Pointer to Another Object
### Own Is A Namespace
A *namespace* is a lookup table.

Each row in the table maps a string name to an object.

Namespaces could be implemented as hash tables.

Names "point" to objects, either *function objects* or other kinds of *objects*.  (Both kinds of objects are the same).
## Magic Slot for Code
Function objects contain a "magic name" that points to a code blob.

The name is entirely implementation-dependent.

![function objects](/assets/js-object-function-object-code-field.png)

## Function Call Syntax
## Object.Create
## New
## Diagram

![objects](/assets/js-object-object-creation-and-new.png)

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
