
---
layout: post
title:  "S/SL Takeaways"
---
# S/SL

S/SL means Syntax Semantic Language.  (See References).

S/SL is described as a minimal syntax for parsing.  

Parsing has been subsumed by Parser Combinators and PEG.

Yet, S/SL still contains a hidden gem.

# Takeaways

- link functions[^mech].

[^mech]: Link functions are called mechanisms in S/SL.  See also, S/SL's types, inputs, outputs and errors.

# Link Functions
Link functions are unimplemented functions.

Link functions are not implemented in S/SL, but are implemented in the base language (I call this a Toolbox Language).

# Dataless Language

In S/SL, there is no data.

There are only _handles_[^enums] to data.

One can declare the existence of data and can move it around, but one _cannot_ specify the implementation of the data in S/SL.

[^enums]: Similar to the concept of enums.

# Typeless Language
S/SL has no built-in types[^builtintypes].

In S/SL, you can declare _handles_[^enums] to types, but you _cannot_ specify how the types are implemented.

# Inputs
Inputs are declared as _handles_.
# Outputs
Outputs are declared as _handles_.
# Errors
Erros are declared as _handles_.

[^buildinttypes]: This is not entirely true, but is a useful approximation for this essay.

# Restricted API To/From Link Functions

S/SL functions can take 0 or 1 parameters (only).

S/SL functions can return 0 or 1 return values.

# Datalessness In Other PLs
It is _possible_ to create data handles in other PLs, but most PLs tend to encourage description of the implementations.

For example, _int_, _float_, _array_, _list_, etc. are examples of data implementations.

S/SL enforces non-implementation of details

# Typelessness in Other PLs
It is _possible_ to create hierarchies of abstract types in other PLs, but this usually tends (psychologically) towards accidental complexity.

S/SL enforces the use of type handles.

# Input in Other PLs

S/SL's simple handles enforce simple description of inputs.

# Output in Other PLs

S/SL's simple handles enforce simple description of outputs.

# Error in Other PLs

S/SL's simple handles enforce simple description of errors.

Many current PLs implement error handling using `throw`, resulting in backtraces of uninteresting details (e.g. essentially the same as core dumps).

Error handles could be used to invoke `throw`, or, better, could be used to provide useful debugging error messages.

# Encouraging Behavior vs Possible Behavior
There seems to be a fine line between PLs that encourage certain paradigms vs. making those behavior possible.

For example, it is _possible_ to write CPS in assembly code, but few programmers bother to do so.

Lifting concepts to make them visible, vs. eliding other concepts, is an important aspect of PL design.

S/SL's use of _handles_ makes the Architectural concepts of a progam visible, while eliding implementation.

# See Also

https://guitarvydas.github.io/2021/01/14/References.html
https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html


<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
