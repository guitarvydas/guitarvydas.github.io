---
layout: post
title:  "Data Cleaving"
---

Programs have _data_.

Let's apply the fractal principle to _data_ and see what emerges.

Let's divide _data_ into two divisions and dig into the divisions more deeply.

Several PLs provide _getters_ and _setters_ for data.


# 1. Set
A _setter_ function creates a piece of data and sets it to some value.

Q: Does the _setter_ check the validity of the information? Or, is that operation moved elsewhere?

Using fractal thinking, it becomes "obvious" what a _setter_ should do.

_Setting_ becomes 2 operations:
# 1a. Validate
# 1b. Raw set

The operations can be pipelined to make a [type stack](https://guitarvydas.github.io/2020/12/09/Type-Stacks.html).

_Setting_ should not be conflated with _validation_.

We are familiar with the concept of _validation_ - many web-based forms use some kind of input validation.


# 2. Query
The concept of _getters_ is not specific enough. 

A person reading the code can see that data is being fetcheded, but not _why_ the data is fetched.

We _get_ data for a reason.

Typically, we want to _query_ the data in some manner.

_Querying_ can be a simple _get_, or, it can be a more involved operation, maybe a  _rule_ involving the value of the data, or a _rule_ involving many values of many data.

_Getting_, also breaks down, fractally, into two operations
# 2a. Raw get
# 2b. Query

The fractal concept has no _bottom_. Each of the above operations can be further sub-divided, recursively[^recur].

[^recur]: We stop sub-diving a problem when the sub-divisions are "good enough" to solve a problem, not when we "hit bottom".

For example, _raw get_ might further be broken into 
1. getting from memory
2. getting from a database.

Likwise, _query_ might be further broken down into 
1. querying information from memory
2. inferring new information based on information from memory.

# Conflation of Get and Set

Many PLs provide _getters_ and _setters_ but don't further specify _how_ the data is validaed nor _why_ the data is fetched. These, otherwise simple, categorizations are hidden in code. The reader needs to _reverse-engineer_ the _validation_ and _querying_ intent from the code.

This kind of code conflation is accidental complexity - the Designer _knew_ how and why he was doing certain operations, but lacked the PL syntax to communicate the Design Intent to future readers of the code.

[_Aside: I argue, in other essays that Architects should invent SCNs to describe their DI._]

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
