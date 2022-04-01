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
There are two ways to create an object
1. Object.create()
2. new
### Object.Create
A method call on the top level Object object.
### New
`var x = new YYY (...)`
The `new` statement calls a "regular" function in a special way...

All methods (functions) are called with a `this` parameter.

Usually, 
```
f.x (y)
```
is converted to
```
call f.%own%.%code% with parameters (f, y)
```
(where `%own%` and `%code%` are names that I invented to represent implementation-dependent ways of getting the function (code) to be called. It is easiest to imagine that the %code% blob is attached to the namespace of the object `f`, but, implementations might optimize this in different ways).

In the case of `new` though,
```
var x = new YYY (...)
```
is converted to a several-step process
1. temp = {} 
2. temp2 = call YYY.%own%.%code% (temp, ...)
3. temp2.%proto% = YYY.%proto%
4. return temp2

This version is supported by compilation rules:
1. if YYY.%own%.%code% uses a `return` statement, return whatever is specified
2. if there is no `return` statement, silently insert `return this` into the exit point of the function (the compiler needs to catch every exit point ; in fact maybe it is just enough to insert a `return this` at the end of every function (the end of the function can only be reached if there are no other `return`s excecuted before reaching the end)).

The above compilation rules are used by *every* function, but only make total sense when called by `new`.  In the common cases, all functions must include a `return` statement.  Any function that does not contain a `return` is deemed to be a `Constructor`.

The above only matters to compiler-writers.  For everyone else, the documentation contains hand-waving references to *functions* and *constructors*.  From a compiler-perspective, *functions* and *constructors* are the same.  The compiler doesn't need to remember which functions are Constructors, it simply treats all function calls as method calls and calls functions differently in the two cases (1. normal, and, 2. `new`).

#### Relationship to Lisp

JavaScript function names aren't simple pointers-to-code, but are pointers-to-objects.  

The objects can be walked to find code.  

This is very Lisp-y.  

In Lisp, functions are *always* anonymous (signified by the keyword `lambda`).

In Lisp *every* symbol (a symbol is just a name, a "handle") contains a set of values.  One of the values might be a `lambda`.

In Lisp[^lisp2], it is *possible* to have a symbol that has more than one kind of value, e.g. a symbol might contain a datum plus a `lambda`

[^lisp2]: In Lisp2, to be exact.  Lisp1s don't allow multiple values for symbols.

### Diagram

![objects](/assets/js-object-object-creation-and-new.png)

### Code Transformation

```
function f (this, x) {
  return 1;
}
```

is converted to

```
function f (this, x) {
  return 1;
  return this;
}
```

#### Call Syntax Transformation
There are two ways to call functions:
```
y.f(3);
```

and
```
var x = new f(3);
```

[*I use `%` like a normal character, like JavaScript uses the `_` character*].

The first version is converted to
```
f.%own%.%code%(y, 3);
```

and, the second version is converted to
```
var %temp% = {%proto%=null, %own%=null}
var %temp2% = f.%own%.%code%(%temp%,3);
%temp2%.%proto% = f.%proto%
var x = %temp2%
```


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
