---
layout: post
title:  "Relations"
---

# Machine Readability
## No Order
- Relational Languages do not imply sequential operation
- No "declaration before use"
## Not Syntax Driven
The syntax of relations is very simple `relation (subject, object)`.  Relations can be emitted (output) in any order.
### This is Important Because...
Emitting machine-readable code is harder when output must be put in some order.

E.G. C requires declaration-before-use, e.g. 
```
void func (a) {
  x = 5;
}
int x; 
``` 
is illegal and must be rewritten as
```
int x; 
void func (a) {
  x = 5;
}
``` 

In this case, the emitter must make sure that `int x;` occurs prior to the function definition.

In more complicated examples, this requires the use of various buffers to memorize code sequences, with a final pass that orders the outputting of buffers

Relations, though, can be emitted in any order - the engine takes care of figuring out the order (for searching).
# Separation of Architecture from Implementation
## Engine
### Exhaustive Search

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
