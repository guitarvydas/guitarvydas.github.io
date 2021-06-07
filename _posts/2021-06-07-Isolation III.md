---
layout: post
title:  "Isolation III"
---
`True isolation` is
+ ```data isolation``` AND
+ ```control-flow isolation```

# CALL / RETURN
CALL/RETURN does not isolate control-flow, it implies sequential operation.

`var x = obj.method (...)` is sequential.

# Relational Programming
Relational programming does not imply sequential operation.

All control flow is handled by the relational engine.

# UNIX Threads

UNIX threads do not imply sequential operation.

Uber control flow is handled by the dispatcher.

# Functions Are Sequential

`fn(a)->b` implies sequential operation.

The parameters are delivered in a "sequential block" (all parameters are delivered at the same time).

The return value is delivered in a "sequential block".

The caller waits for a result.

# Concurrency vs. Parameters

Note that sequentialism leaks into parameter passing.

In sequential programming, _all_ parameters must be delivered at the same time.

In concurrent programming, parameters can be delivered 
- _at any time_ 
- _in any order_
- _individually_.

Grouping parameters together and grouping return values together is the exception, not the rule, in concurrent programming.

# Lifetime - Forever vs. Live-Then-Die

The caller does/can not care if the callee 
- (a) lives forever, or,
- (b) lives-then-dies.

(a) is server-like.

(b) is function-like.

# Need to Know
Saying `x.fn(...)` implies that you know too much about "x". 

That knowledge is hard-wired into the calling code and makes it hard to change later, aka accidental dependency.

Suggestion: all methods have only one calling syntax and all methods have the _same_ parameter list syntactically, with the _same type_ (!).

## Type Checking

The suggestion is not to delete type-checking, but to move it elsewhere.

We _already_ do this with compilers -> opcodes.

Compilers can be viewed as type filters that strip away semantic information to produce untyped opcodes.

# Choice

In `var x = obj.method (...)`, you do not get to choose whether the operation is concurrent or sequential.

The choice is made for you and baked into your code (aka accidental dependency (aka accidentally not-isolated)).

# Further Suggestion

Suggestion: code cannot _call_ a method in an object.

Code can only _send_ information to its _parent_.

The _parent_ can _choose_ to _send_ this information to another child for further processing.

I.E. a function cannot _name_ other objects and methods.

# Software Components

Software components can contain code.

Software components can only _send_ information upwards to their _parents_, or, they can _send_ commands to their children.

Cross-talk is not allowed.

Cross-talk produces non-scalable code.

Corollary: components cannot communicate directly with their peers.

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
