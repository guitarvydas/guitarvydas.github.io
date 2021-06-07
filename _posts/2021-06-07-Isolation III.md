---
layout: post
title:  "Isolation III"
---
`True isolation` is
```data isolation```
+ 
```control-flow isolation```

# CALL / RETURN
CALL/RETURN does not isolate control-flow, it implies sequential operation.

`var x = obj.method (...)` is sequential.

# Relational Programming
Relational programming does not imply sequential operation.

All control flow is handled by the engine.

# UNIX Threads

UNIX threads do not imply sequential operation.

Uber control flow is handled by the dispatcher.

# Functions Are Sequential

`fn(a)->b` implies sequential operation.

The parameters are delivered in a "sequential block" (all parameters are delivered at the same time).

The return value is delivered in a "sequential block".

The caller waits for a result.

# Lifetime - Forever vs. Live-Then-Die

The caller does/can not care if the callee 
- (a) lives-then-dies, or, 
- (b) lives forever.

(a) is function-like

(b) is server-like.

# Need to Know
Saying `x.fn(...)` implies that you know too much about "x". 

That knowledge is hard-wired into the calling code and makes it hard to change later, aka accidental dependency.

Suggestion: all methods have only one calling syntax and all methods have the _same_ parameter list syntactically, with the _same type_.

## Type Checking

The suggestion is not to delete type-checking, but to move it elsewhere.

We _already_ do this with compilers->opcodes.

Compilers can be viewed as type filters that strip away semantic information to produce untyped opcodes.

# Choice

In `var x = obj.method (...)`, you do not get to choose whether the operation is concurrent or sequential.

The choice is made for you and baked into your code (aka accidental dependency (aka accidentally not-isolated)).

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
