---
layout: post
title:  "Type DSL (SCN)"
---

# Introduction

In this essay, I describe a mini-DSL that is used in a larger project[^1]. 

[^1]: A Diagram to Code transpiler called Arrowgrams.

This SCN is used to define and implement the types used in the larger project

The implementation is complicated-enough that the code to implement the types obscures the bare essence of the type system.

The intent of this sub-project is to build the type system in layers, each layer revealing only the bare essence (at that layer) and eliding details in lower layers.

Details are elided, but not discarded.

This technique differs from the more common technique of using a GPL (General Purpose Language), like Python, etc.

In essence, there is nothing new here, I simply rearrange existing technologies and emphasize layering using FDD (Failure Driven Design) and PEG.

This essay consists of 2 major parts
1. Type SCN
2. Philosopy.

I present the SCN first, then discuss the philosophy behind the design.

## SCNs

I call mini-DSLs "SCNs". SCN means "Solution Centric Notation".

## Type SCN

The bare essence of this type system is built on only 6 primitive kinds of definitions:
```
id = { ... ... ...}         --> class with fields def
id = :bag ...               --> bag def
id = :string ...            --> string def
id = :map ...               --> map def
id = | ... | ... | ...      --> compound type def
id = '...' |  '...' | ...   --> enum def
```

Comments begin with "%" and continue to the end of the line.

Here `...` represents single names[^2][^3].

[^2]: and the last "..." means "more of the same".

[^3]: I employ the principles of "layering" even here. This definition is not rigorous, but one can interpolate its meaning. This definition avoids creating a wall of detail.

Spaces separate names (commas and semi-colons are not used).

Originally, the syntax was parsed manually. To aid such manual parsing, I designed the syntax to contain _left handles_.  Every construct begins with "id =" and the next token (the third token) uniquely determines the kind of construct being used, e.g. `{`, `:bag`, `:string`, `:map`, `|` and `'`.

SCN principle: some of the above constructs have become obsolete over time. I leave those constructs in, since the definition is "good enough" to get the job done, and, in some way shows the provenance from original ideas to final reality.  Future maintainers might choose to prune the definition, but no time is wasted in doing so at the moment.

# Example Specification
The spec below[^6] can be found in [exprtypes.dsl](https://github.com/bmfbp/bmfbp/blob/main/build_process/esa-transpiler/exprtypes.dsl).

[^6]: Motivation: "esa" means Encapsulated Software Artefact.  "When" and "situations" can be thought of as "passes".

I've removed all comments from the SCN below, for clarity. The comments remain in the original source (in the above github).

Note that the full type system for this sub-project can be described using a simple SCN consisting of about 6 main rules.

[N.B. This is code that forms a sub-portion of a larger project, copied verbatim.]

<u>Reading 1</u>: the first line declares a type called "esaprogram". The type contains 4 fields "typeDecls", "situations", "classes" and "whenDeclarations".

<u>Reading 2</u>: the line `name = :string` declares that "name" has a type that is a foreign type. It is a foreign (external) type called ":string". The type system says nothing about the foreign type ":string".  No methods for the foreign type ":string" are defined. The foreign type ":string" is built-in to the transpiler.  The name ":string" is historical. I might choose to call it ":foreign" today.

Of note: All types in the type system boil down into one of the builtin types, ":string" and ":map"[^4]. 

Of note: All types in the type system are defined in terms of 2 basic types.

Of note: There are no variable names in this specification. Type names are unique. In places where the same name might appear more than once, a new typename is created. See `methodDeclaration` which ultimately contains two `:strings`.  The first is called `esaKind` and the second is called `name`. The SCN engine sorts out the types for `esaKind` and `name`. The SCN engine does the work automatically. The Architect needs only ensure that coincident types have unique names. Usually the layered name (`esaKind` in this case) is a more meaningful description, from an Architectural perspective, than the final name (`:string` in this case).

[^4]: As it happens, ":bag" is not used at all. I might choose to deprecate ":bag" in future versions of this SCN.  This would have the satisfying property of making the SCN _even simpler_ - 5 rules instead of 6. (Currently, I believe that we need only two types - _thing_ and _list of thing_ - at the Architectural level.  All other types are implementation details and should not appear anywhere but at the bottom-most layer of a design).

The builtin type ":map" is meant to be a collection. It's name is historical. I might choose to call it something different in future versions[^5]. Again, this is not an exercise in perfecting the SCN, but an exercise in getting things done. I will leave ":map" alone for now.

[^5]: Currently, I use the syntax [xyz] to signify  a collection of xyz.  Brackets `[]` mean "collection of".

The type system defined below is not necessarily "easy" to understand. Future maintainers must, still, understand what is going on, much like they already do when maintaining any code base. The type system, though, has much of the GPL details elided and is "easier to read" than a wall of GPL code.  This type system shows only Architectural details (at this level).  The Type SCN focuses the Architects' efforts on software architecture only, instead of on the conflation of architecture+implementation.

The SCN transpiles the specification to a GPL. In this case, [exprtypes.dsl](https://github.com/bmfbp/bmfbp/blob/main/build_process/esa-transpiler/exprtypes.dsl) is transpiled into [exprtypes.lisp](https://github.com/bmfbp/bmfbp/blob/main/build_process/esa-transpiler/exprtypes.lisp). It should be possible to transpile to some other base language (I call it a _toolbox language_), such as Python.


```
esaprogram = { typeDecls situations classes whenDeclarations  }

typeDecls = :map typeDecl
situations = :map situationDefinition
classes = :map esaclass
whenDeclarations = :map whenDeclaration

typeDecl = { name typeName }
situationDefinition =| name
esaclass = { name fieldMap methodsTable }

whenDeclaration = { situationReferenceList esaKind methodDeclarationsAndScriptDeclarations }
situationReferenceList = :map situationReferenceName
situationReferenceName =| name

methodDeclarationsAndScriptDeclarations = :map declarationMethodOrScript
declarationMethodOrScript =| methodDeclaration | scriptDeclaration

methodDeclaration = { esaKind name formalList returnType }

scriptDeclaration = { esaKind name formalList returnType implementation }

returnType = { returnKind name }
returnKind = 'map' | 'simple' | 'void'
formalList = :map name

esaKind =| name
typeName =| name

expression = { ekind object }
ekind = 'true' | 'false' | 'object' | 'calledObject'
object = { name fieldMap }
fieldMap = :map field
field = { name fkind actualParameterList } 
fkind = 'map' | 'simple'
actualParameterList = :map expression
name = :string

methodsTable = :map declarationMethodOrScript


externalMethod = { name formalList returnType }
internalMethod = { name formalList returnType implementation }
implementation = :map statement

statement =| letStatement | mapStatement | exitMapStatement | setStatement | createStatement | ifStatement | loopStatement | exitWhenStatement | callInternalStatement | callExternalStatement | returnTrueStatement | returnFalseStatement | returnValueStatement

letStatement = { varName expression implementation }
mapStatement = { varName expression implementation }
exitMapStatement = { filler } 
setStatement = { lval expression }
createStatement = { varName indirectionKind name implementation }
ifStatement = { expression thenPart elsePart }
loopStatement = { implementation }
exitWhenStatement = { expression }
returnTrueStatement = { methodName }
returnFalseStatement = { methodName }
returnValueStatement = { methodName name }
callInternalStatement = { functionReference } 
callExternalStatement = { functionReference }

lval =| expression
varName =| name
functionReference =| expression
thenPart =| implementation
elsePart =| implementation

indirectionKind = 'indirect' | 'direct'

methodName =| name
filler =| name
```

A working diagram is in [exprtypes.drawio](https://github.com/bmfbp/bmfbp/blob/main/build_process/esa-transpiler/exprtypes.drawio).

# Philosophy

## Previous Attempts

### GPLs

Most current GPLs provide only 2 layers:
1. User definitions layer
2. Implementation layer.

### OOP

OOP is an attempt to provide more layers in data design, but OOP provides the programmer(s) only with the basic tools (the "assembler") for doing so. Some programmers design and display their systems in layers, most don't.

In this approach, we define a _notation_ for our top layer, then apply various tools to implement the _notation_ in layers.

The intent is that every layer contain only the bare essence of what is needed, eliding details to other layers.

Most PLs already have these capabilities (esp. when mixed with AOP).

## Syntax is cheap.

I augment the use of GPLs with the use of PEG parsing technologies. 

I invent syntaxes and use them as light-weight notations.

I favour the creation of many syntaxes for a single project, instead of sticking to the syntax given by a single GPL.

## Architecture

This essay describes a way of writing concrete Software Architecture.

The goal of Software Architecture is [Design Intent](https://guitarvydas.github.io/2020/12/09/DI-Design-Intent.html).

## Common Lisp

 Common Lisp is a GPL that contains everything-but-the-kitchen-sink and I often use it as my _toolbox language_. 

## JavaScript

 JavaScript is a close second to CL. 

## Python

 Python is more popular than either of the above languages, at the moment, but Python emphasizes a syntax geared towards human-readability (which makes it harder - not impossible - to automatically emit code from a transpiler).

## Portability

SCNs can produce portable code - code in any GPL - if appropriate technology is used (e.g. PEG parser generators)

## Meta-Programming

Portability is also called `meta-programming`. The concept is that a single description source can be used to create code in any language.

This is what `compiler technologies` already do. Compilers input a GPL text and output assembler code of various forms.

Compilers are limited forms of meta-programming.

Compiler technologies include techniques for optimizing code.  These techniques could be directly applied to optimizing code generated by SCN transpilers.

## Macros

Macros, such as Lisp macros, M4, and C macros, are meta-programming wannabes.

## Functions, Referential Transparency

Referentially-transparent functions are restricted forms of macros. See the above discussion of meta-programming.

## Referential Transparency for Hardware

TTL hardware designers used the phrase "pin compatible" to refer to component substitution.

Hardware often used _sockets_ to house hardware ICs. 

One could literally pull out an IC and plug another one into the socket.  

One could buy _chip pullers_ which made it easier to pull chips (ICs) out of sockets.

## Pragmas and #ifdef, 

Pragmas and C's #ifdef are limited forms of meta-programming. See the above discussion.

## CL \*features\*
CL's [\*features\*](http://www.lispworks.com/documentation/lw50/CLHS/Body/v_featur.htm) feature is a limited form of meta-programming.  See the above discussion.


## Machine readability vs. human readability

 I suggest that, for building SCN transpilers, it is more convenient to use a language - a `toolbox language` - that is "harder" to read and emphasizes machine-readability over human-readability.

## PEG

PEG means "parsing expression grammar".

PEG is a pattern matcher notation, like REGEXP. 

PEG is better than REGEXP for certain kinds of patterns, e.g. multi-line structures, vs. single-line matches.

PEG makes it possible to treat syntax as a commodity. Syntax is cheap.

I consider this "Type SCN" (mini-DSL) to be a notation.

This essay shows how I use PEG to implement the notation.

The Type SCN remains a "hard" problem. PEG makes it possible to split the problem into two halves
1. The Notation
2. The (Architectural) Use of the Notation.

Using PEG makes it possible to automate the notation, wheres the _thinking_ part - Architecture - is not automated.

The _thinking_ part is, though, "easier" to think about because it is not tangled up with implementation details.

## No Variable Names

Note that the SCN notation, above, uses no variables names.

I use identifiers for types and do not require variable names.

In the infrequent case that type names clash, new names are invented for the types to keep them unique from one another.  The SCN engine sorts out the final types for all names.

I use names that are essentially complete phrases that, hopefully, express my DI .  [_Note that, I am the Architect, readers need to read and understand what I was thinking. I believe that any problem solution has many possible forms.  No solution is "perfect", the only goal is to allow my readers to understand what I chose to do._]

## Foreign Types & Dataless Programming Languages

Programming a computer involves two domains:
1. The Data
2. The Control Flow.

Most GPLs conflate both domains into a single language.

I try to keep the two domains separate
1. The Data domain is not allowed to express control flow construction.
2. The Control Flow domain is not allowed express data construction.

Note that _some_ operations, such as setters and getters, fall into the Data domain but are more like control flow constructs (for example, if-then-else oriented only at data description).

_Case_ on _type_ falls into the data domain (in fact, _case_ on _type_ is the main feature of method dispatch in OO).

Other kinds of control flow fall into The Control Flow domain.  An SCN for control flow needs to be _dataless_.

It _is_ possible to define languages that are dataless. A _dataless_ language can move data around using _handles_, but cannot "look into" data objects nor describe how they are constructed. We have seen versions of these concepts in windowing systems, where the contents of _window_ data structures are opaque (handles to opaque data structures).

S/SL - Syntax / Semantic Language - is a dataless language. S/SL deals only with the domain of control flow for parsing, leaving all data access and construction to foreign modules (called _mechanisms_).

## FDD - Failure Driven Development

I use the tenets of FDD: "automate as much as possible". I automate code generation in preference to writing code manually.

## Pattern Matching (and FP, Haskell, Elm)

Parsing is pattern matching.

FP uses pattern matching.

Parsing is _solely_ focused on Pattern Matching.

Haskell is an FP GPL.  Haskell is _not_ only focused on Pattern Matching.

Likewise, Elm uses pattern matching, but provides other kinds of functionality, in addition to pattern matching.

## Other Philosophical Points

### Diff

With respect to automating code generation, `diff` could be used to help create variants of code instead of simply recording differences.

### DRY

DRY means "Don't Repeat Yourself".

The Software Architect should not be forced to apply DRY principles manually.  `Diff` should automate the process of DRY detection.

# GitHub

[esa-transpiler2](https://github.com/bmfbp/bmfbp/tree/main/build_process/esa-transpiler2)

# Larger Project

This type SCN is part of a larger project [Arrowgrams](https://github.com/bmfbp/bmfbp/tree/main).

The goal of the larger project was to compile diagrams into executable code.  The diagrams were drawn in [draw.io](https://app.diagrams.net), exported as a subset of SVG, then compiled into Common Lisp code.

# See Also

[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html)
[AOP](https://en.wikipedia.org/wiki/Aspect-oriented_programming)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
