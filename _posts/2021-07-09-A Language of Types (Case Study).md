---
layout: post
title:  "Case Study - A Language of Types"
---

In this essay, I discuss a simple language for constructing type systems.

The language boils down into some 5 operations.

The language has been used to create a diagram transpiler and a runtime for transpiled diagrams.

I will discuss each "type operation" below

# SCN

In the following, I use the term "SCN" to mean Solution-Centric Notation, a form of mini-DSL.

# Github

A manifestation of this language can be found in [exprtypes.html](https://github.com/bmfbp/bmfbp/blob/main/build_process/esa-transpiler2/exprtypeslisp.html) with support code in [stack-dsl](https://github.com/guitarvydas/stack-dsl).

The SCN was first built in CL (Common Lisp) using the [esrap](https://scymtym.github.io/esrap/) PEG parsing library.

Later, the SCN was re-written in Ohm-JS and Glue and resides in [exprtypes.html](https://github.com/bmfbp/bmfbp/blob/main/build_process/esa-transpiler2/exprtypeslisp.html), as mentioned above.

[Overiew of Arrowgrams](https://guitarvydas.github.io/2021/07/09/Arrowgrams.html)

[Overview of Type SCN](https://guitarvydas.github.io/2021/07/05/Type-DSL-(SCN).html)

# Type SCN Operations

The bare essence of this type system is built on only 6 primitive kinds of definitions:
```
id = { ... ... ...}         --> class with fields def
id = | ... | ... | ...      --> compound type def
id = '...' |  '...' | ...   --> enum def
id = :bag id2               --> bag def
id = :string                --> string def
id = :map id2               --> map def
```

Comments begin with "%" and continue to the end of the line.

Here `...` represents single names[^2].

[^2]: and the last "..." means "more of the same".

Spaces separate names (commas and semi-colons are not used).

Originally, the syntax was parsed manually. To aid such manual parsing, I designed the syntax to contain _left handles_.  Every construct begins with "id =" and the next token (the third token) uniquely determines the kind of construct being used, e.g. `{`, `:bag`, `:string`, `:map`, `|` and `'`.

SCN principle: some of the above constructs have become obsolete over time. I leave those constructs in, since the definition is "good enough" to get the job done, and, in some way shows the provenance from original ideas to final reality.  Future maintainers might choose to prune the definition, but no time is wasted in doing so at the moment.

## Type Operation - Class With Fields
```
id = { ... ... ...}         --> class with fields def
```

This operation create a type with named fields.

Each name is a type unto itself.

Name clashes are not allowed. (The same field name must not be used more than once in a given definition)

Name clashes are resolved - by the programmer - by inventing new type names and equating them to other types, for example
```
a = { b b }
```
would be resolved by manually writing the above as:
```
a = { y z }
y =| b
z =| b
```
It has been found, in practice, that name clashes occur infrequently


## Type Operation - Compound Type
```
id = | id2 | id3 | ...      --> compound type def
```
This operation creates a type that is the union of the given types (in this case, id2, id3, etc.)

### Type Operation - Equating Types
```
id = | id2
```
Types can be equated by writing degenerate compound type definitions.

## Type Operation - Enum Type
```
id = 'k1' |  'k2' | ...   --> enum def
```

This operation creates an enum type that holds exactly one of the above constants.

## Type Operation - Foreign :string Type
```
id = :string            --> string def
```
A builtin type, currently called ":string"[^1], is a _handle_ to some opaque type that is implemented in the supporting toolbox language (aka base language).

[^1]: I would suggest a different name, such as ":foreign" for future versions of this SCN.

## Type Operation - Foreign :map Type
```
id = :map id2              --> map def
```
This operation creates an ordered list of type id2. The "ordered list type" (currently called ":map" for historical reasons[^map]) is built into the type transpiler, whereas the object type, id2, can be any type defined in the specification (or can be one of the builtin types.)

[^map]: I tried to avoid the use of the word "list" since it tends to mean a specific implementation.  Probably ":collection" might be a better name than ":map", albeit longer and "harder to type".

For example, a list of a list of X might be defined as:
```
a = :map b
b = :map X
X = ...
```
## Type Operation - Foreign :bag Type
```
id = :bag id2               --> bag def
```
This operation creates an unordered list of type id2, akin to ":map" above.

It is not clear whether this type is actually needed, since unordering is "just" an optimization.

I _strongly_ suggest that Architecture (DI) and Optimization be separated and not be conflated together.

# Transpiling to Primitive Engine Operations
The Type SCN is transpiled into a set of primitive operations[^op].

[^op]: Much like how a compiler compiles a programming language into a set of assembler operations.

The operations are implemented / interpreted by an engine.

Currently, the engine is written in CL (Common Lisp), but I believe that any toolbox language could be used (e.g. Python, JS, etc.)

## Engine Primitive Operators
### Pushing Data Onto A Stack
Typecheck that source (the datum) meets requirements of destination (the stack).

Note that "typecheck" means to simply compare names. (Shallow compare, no need for deep compare).

### Setting a Field
Typecheck that source (the datum) meets requirements of destination (field of type).
### Appending to a List
Typecheck that source (the datum) meets requirements of destination (element type of the list).
### Output
Pop datum from stack. Push popped value onto output stack (of same type).
### New
Create and push an empty stack entry.
### Pop
Remove one item from the given stack. Check for underrun.
### Coercion
From a builtin type to a SCN-defined type.

Programmer-specified coercion.

## Low-Level Routines / Scripts

## Signatures

NIY: Each routine specifies a post-condition which describes the change in the various stack depths.

NIY: A routine must consume (pop) all of its input parameters and push one (or more) output results.  [_This is not currently implemented.  I only check stack depth when an app completes operation (an app must leave stack depths as it found them, with no net change).  In practice, this simple check turned out to be sufficient._]

[_In future variants: an operation could be added to the engine to push/modify stack signatures upon routine entry._]

A _signature_ is:
1. a set of input parameters
2. a set of output parameters.

Signatures can be checked at runtime (dynamic checking). I imagine that signatures could also be pre-checked (static checking).

Signatures annotate sequences of operations (aka "functions", aka "routines"). I call these sequences "scripts".

## Scripts and Methods

Operations are performed in groups, much like groups of assembler operations perform the bodies of functions.

Operation sequences can be specified:
1. internally to the SCN (_scripts_)
2. externally outside of the the SCN (_foreign_).

This concept is "nothing new".  It is akin to writing the code for a function in the same file as it is to be used, versus, writing the code for the function in some other file, then importing the file.  I call these _scripts_ and _methods_ respectively. (In other words: imported functions are called _methods_, non-imported functions are called _scripts_).

To further belabor the point: code can be written in the SCN, _or_, code can be written in any other language, say, Python. Code written in the SCN would be called a _script_ whereas code written in Python would be called a _method_.  

Code written in the SCN must not name-clash with code written in Python (for now).

Imagine (for now) that _all_ code is transpiled into the target language, say Python, and glued together to make the final app.

## Watermarking
### Memorizing Stack Depths
The engine memorizes all stack depths before executing an app.

NIY: The engine memorizes all stack depths before executing a primitive operation.

### Checking Stack Depths
After executing an app, the engine checks that all stacks have returned to their pre-operation depths.
NIY: After executing a primitive operation, the engine checks that all stacks have returned to their pre-operation depths modified as appropriate by the script's signature.

In the current code this check is implemented by "%memoStacks()" and "%memoCheck()"[^c]

[^c]: "%" is just another legal character in identifiers. The current implementation uses CL (Common Lisp) which allows many characters as parts of identifiers. In come other PLs, "%" is an operator and cannot be used as part of an identifier - in which case we need to transliterate (name-mangle) identifiers that contain "%" characters into something acceptable.
# Type Checking
## Type Descriptors
A type is defined by
1. its name
2. information dependent on the type of the type (e.g. a list of fields, a list of enums, etc.)

## Type Checking
A Type is equivalent to another Type if it has the same name.

We can avoid the need for deep type checks by recognizing that
1. each type has a unique name
2. type checking needs only to be done during push, set-field and append operations.

## Stacks
Each type, including the builtin types, is assigned 2 stacks
1. An input stack
2. An output stack.

The input stack is used for sending parameters (of the given type) into a routine and for temporaries storage.

The output stack is used for returning a value (of the given type) from a routine.

In popular GPLs (General Purpose Languages) _all_ types use [the same stack](https://guitarvydas.github.io/2020/12/25/The-Stack.html) (and [desired result](https://guitarvydas.github.io/2020/12/27/The-Stack-2.html)). This concept was borne out of the 1950's tendency to optimize storage - a concern that is no longer an issue.

The multiple stacks - 2 for each type - can be implemented using a heap.

[_In future variants: it might be desirable to separate temporary storage from input parameters, requiring 3 stacks for every type. It is possible to reduce the number of stacks to 1 per type, but that is only an optimization and will unnecessarily hide architectural details._]

Each stack contains a type descriptor that describes the type of element(s) in the stack.

# Common Lisp Implementations
## Type Operation - Class With Fields
```
typeDecl = { name typeName }
```
is transpiled into
```
(proclaim '(optimize (debug 3) (safety 3) (speed 0)))(in-package "CL-USER")

(defclass typeDecl (stack-dsl::%compound-type)
(
(%field-type-name :accessor %field-type-name :initform "name")
(name :accessor name)

(%field-type-typeName :accessor %field-type-typeName :initform "typeName")
(typeName :accessor typeName)
)
(:default-initargs :%type "typeDecl"))
(defclass typeDecl-stack (stack-dsl::%typed-stack) () ())
(defmethod initialize-instance :after ((self typeDecl-stack) &key &allow-other-keys)
  (setf (stack-dsl::%type-list self) "typeDecl"))


(stack-dsl::%ensure-existence 'name)
(stack-dsl::%ensure-existence 'typeName)
(stack-dsl::%ensure-existence 'typeDecl)

(defclass %map-stack (stack-dsl::%typed-stack) ())
(defclass %bag-stack (stack-dsl::%typed-stack) ())
(defmethod initialize-instance :after ((self %map-stack) &key &allow-other-keys)
  (setf (stack-dsl::%element-type self) "%map"))(defmethod initialize-instance :after ((self %bag-stack) &key &allow-other-keys)
  (setf (stack-dsl::%element-type self) "%bag"))

(defclass environment ()
((%water-mark :accessor %water-mark :initform nil)
(input-name :accessor input-name :initform (make-instance 'name))
(output-name :accessor output-name :initform (make-instance 'name))
(input-typeName :accessor input-typeName :initform (make-instance 'typeName))
(output-typeName :accessor output-typeName :initform (make-instance 'typeName))
(input-typeDecl :accessor input-typeDecl :initform (make-instance 'typeDecl))
(output-typeDecl :accessor output-typeDecl :initform (make-instance 'typeDecl))
))

(defmethod %memoStacks ((self environment))
(setf (%water-mark self)
(list
(stack-dsl::%stack (input-name self))
(stack-dsl::%stack (output-name self))
(stack-dsl::%stack (input-typeName self))
(stack-dsl::%stack (output-typeName self))
(stack-dsl::%stack (input-typeDecl self))
(stack-dsl::%stack (output-typeDecl self))

)))
  

(defparameter *stacks* '(
input-name
output-name
input-typeName
output-typeName
input-typeDecl
output-typeDecl

))

(defmethod %memoCheck ((self environment))
 (let ((wm (%water-mark self)))
  (let ((r (and
	   
(let ((in-eq (eq (nth 0 wm) (stack-dsl::%stack (input-name self))))
      (out-eq (eq (nth 1 wm) (stack-dsl::%stack (output-name self)))))
  (and in-eq out-eq))
(let ((in-eq (eq (nth 2 wm) (stack-dsl::%stack (input-typeName self))))
      (out-eq (eq (nth 3 wm) (stack-dsl::%stack (output-typeName self)))))
  (and in-eq out-eq))
(let ((in-eq (eq (nth 4 wm) (stack-dsl::%stack (input-typeDecl self))))
      (out-eq (eq (nth 5 wm) (stack-dsl::%stack (output-typeDecl self)))))
  (and in-eq out-eq)))))
   (unless r (error "stack depth incorrect")))))
```

Of note:
- typeDecl is defined as a class
- the typeDecl class contains two fields "name" and "typeName"
- the class definition of typeDecl contains information _about_ the type - a type descriptor, e.g. its name "typeDecl"
- each field contains a type descriptor that describes the element types of the corresponding fields
- two subordinate classes are declared - input-typeDecl and output-typeDecl
- a stack class - typeDecl-stack[^dash] - is declared
- various bookkeeping functions are declared ("%ensureExistence", "%memoStacks" and "%memoCheck")
- various bookkeeping variables are declared ("\*stacks\*")
- a bookkeeping class is declared ("environment").

The bookkeeping details matter little. The details depend on the transpiler implementor (in this case, me). The details add a lot of [noise](https://guitarvydas.github.io/2021/03/17/Details-Kill.html) to the implementation 

[^dash]: Note that "-" is just another valid character for identifiers.  The full name is "typeDecl-stack" in this case. In some languages, we might need to employ name-mangling in the transpiler to produce "typeDecl_stack" as the identifier.
## Type Operation - Compound Type
```
statement =| letStatement | mapStatement 
```
is transpiled into
```
...
(defclass statement (stack-dsl::%compound-type) () (:default-initargs :%type "statement"))
(defmethod initialize-instance :after ((self statement) &key &allow-other-keys)
  (setf (stack-dsl::%type-list self) '( "letStatement" "mapStatement")))
(defclass statement-stack (stack-dsl::%typed-stack) () (:default-initargs :%element-type "statement"))
...
```
Note that the types "letStatement" and "mapStatement" are defined elsewhere.

[This example has been elided for brevity, the actual code contains more alternations].

### Type Operation - Equating Types
```
situationDefinition =| name
```
is transpiled into
```
...
(defclass situationDefinition (stack-dsl::%compound-type) () (:default-initargs :%type "situationDefinition"))
(defmethod initialize-instance :after ((self situationDefinition) &key &allow-other-keys)
  (setf (stack-dsl::%type-list self) '( "name")))
(defclass situationDefinition-stack (stack-dsl::%typed-stack) () (:default-initargs :%element-type "situationDefinition"))
...
```
## Type Operation - Enum Type
```
returnKind = 'map' | 'simple' | 'void'
```
is transpiled into:
```
...
(defclass returnKind (stack-dsl::%enum) () (:default-initargs :%type "returnKind"))
(defmethod initialize-instance :after ((self returnKind) &key &allow-other-keys)
  (setf (stack-dsl::%value-list self) '("map" "simple""void")))
(defclass returnKind-stack (stack-dsl::%typed-stack) ())
(defmethod initialize-instance :after ((self returnKind-stack) &key &allow-other-keys)
  (setf (stack-dsl::%element-type self) "returnKind"))
...
```

N.B. they types "map", "simple" and "void" are defined elsewhere.
## Type Operation - Foreign :string Type
```
name = :string
```
transpiles into
```
...
(defclass name (stack-dsl::%string) () (:default-initargs :%type "name"))
(defclass name-stack (stack-dsl::%typed-stack) ())
(defmethod initialize-instance :after ((self ~a-stack) &key &allow-other-keys)
  (setf (stack-dsl::%element-type self) "name"))
...
```

## Type Operation - Foreign :map Type
```
implementation = :map statement
```
transpiles into:
```
...
(defclass implementation (stack-dsl::%map) () (:default-initargs :%type "implementation"))
(defmethod initialize-instance :after ((self implementation) &key &allow-other-keys)  ;; type for items in map
  (setf (stack-dsl::%element-type self) "statement"))
(defclass implementation-stack(stack-dsl::%typed-stack) ())
(defmethod initialize-instance :after ((self implementation-stack) &key &allow-other-keys)
    (setf (stack-dsl::%element-type self) "implementation"))
```
## Type Operation - Foreign :bag Type
```
implementation = :map statement
```
transpiles into:
```
...
(defclass implementation (stack-dsl::%bag) () (:default-initargs :%type "implementation"))
(defmethod initialize-instance :after ((self implementation) &key &allow-other-keys)  ;; type for items in map
  (setf (stack-dsl::%element-type self) "statement"))
(defclass implementation-stack(stack-dsl::%typed-stack) ())
(defmethod initialize-instance :after ((self implementation-stack) &key &allow-other-keys)
    (setf (stack-dsl::%element-type self) "implementation"))
...
```
Note: :bag does not appear in exprtypes.dsl. As mentioned earlier, ":bag" can be deprecated and replace by ":map".
# Relationship to FDD (Failure Driven Development)
[FDD](https://guitarvydas.github.io/2021/04/23/Failure-Driven-Design.html) is based on the notion that most software fails, especially during development.

When our application "works", we move on to another project.

From this perspective, one wants to recognize, fix and continue from failure as quickly as possible.

One of the techniques for handling FDD is automation. 

Automate as much as possible. Push a button to rebuild everything.

Fix, push a button, continue.

I consider Type Systems as tools for thought - way to brainstorm and perfect applications.

Defining a Type SCN is a crucial step in automating design. (The other crucial step would be to define a Control Flow SCN).

# Relationship to Transpilation

Transpilation - converting one source file into different source - is an enabling technology for automation.
	

# Relationship to DI

This Type SCN fits the goals of [DI](https://guitarvydas.github.io/assets/2021-04-11-DI/index.html).

# Relationship to Architecture

I feel that the phrase "Software Architecture" has been watered down and means many different things.

I use the phrase "DI".

See the above section about DI.



# Relationship to Concatenative Languages
This Type Language is 
- stack based
- has no syntax for parameters
- treats input parameters and output parameters equivalently
- treats exceptions as just another output parameter
- allows checking of stack depths.

# Relationship to Type Checking
Type checking engine <= type checker VM code
Type checking engine <= VM code executed at "runtime".
The definition of "runtime" is relative.  In this case, we mean "runtime" of the type-checker, not "runtime" of the final app.
Currently, type-checking is a block of "ad-hoc" code. 

A type checker is an "interpreter" (!). 

Type-checker code transpiles an app into a more-efficient app by pre-checking static types.

Type-checking is a continuum. At one end of the continuum is what we call "dynamic type checking" - checking that is done at runtime (of the app). At the other end of the continuum is what we call "static type checking" - checking that is performed before the app is executed.  

Static type checking optimizes the app, so that the app does not need to check types when it is executed (app runtime).

Then, there is the concept of "strong typing" vs. "weak typing". This concept is _orthogonal_ to the concept of _when_ the typecheck is performed (static vs. dynamic). "No typing" is just an extreme form of "weak typing". [_Corrolary: Dynamic Typing does not necessarily mean "no typing"._]

Type Checking conflates too many operations, in my opinion.  This notation splits the simple part of checking numbers of input parameters and output parameters away from the larger notion of type checking.

# See Also

[An earlier essay on this subject](https://guitarvydas.github.io/2020/12/27/The-Stack-2.html)
[toolbox language](https://guitarvydas.github.io/2021/03/16/Toolbox-Languages.html)
[toolbox language 2](https://guitarvydas.github.io/2021/04/28/Toolbox-Languages-(2).html)
[DI](https://guitarvydas.github.io/assets/2021-04-11-DI/index.html)
[DI Basic Tenet](https://guitarvydas.github.io/2020/12/09/DI-Design-Intent.html)
[DIL](https://guitarvydas.github.io/2021/05/28/DIL-(Design-Intent-Language).html)
[exprtypes.html](https://github.com/bmfbp/bmfbp/blob/main/build_process/esa-transpiler2/exprtypeslisp.html)
[esrap](https://scymtym.github.io/esrap/) 
[Overview of Type SCN](https://guitarvydas.github.io/2021/07/05/Type-DSL-(SCN).html)
[Overiew of Arrowgrams](https://guitarvydas.github.io/2021/07/09/Arrowgrams.html)
[the same stack](https://guitarvydas.github.io/2020/12/25/The-Stack.html)
[FDD](https://guitarvydas.github.io/2021/04/23/Failure-Driven-Design.html)
[desired result](https://guitarvydas.github.io/2020/12/27/The-Stack-2.html)
[Blog](https://guitarvydas.github.io)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
