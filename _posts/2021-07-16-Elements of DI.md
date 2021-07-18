---
layout: post
title:  "Elements of DI (WIP)"
---

- values
  - object
  - collection of object
- components
  - parameter delivery (inputs)
  - invocation (N.B. separate from input/output delivery)
  - result delivery (outputs)
  - run forever by default
- message passing
- RID - relative ID's (hierarchical organization of components and hierarchical message passing)
- Sections
  - type description
  - signatures
  - implementation
  - foreign functions
  - design rules
- Dispatcher

# DI
DI means Design Intent (often called Architecture)

# SCN

SCN means Solution Centric Notation.  

A notation is like a light-weight DSL.

A DSL is like a GPL, but specialized.

A DSL is targetted at a specific sub-problem, but generalized. For example REGEXP is a DSL for pattern-matching strings.  For example SQL is a DSL for database querying.

A *notation* is specialized to a specific problem / project.  A *notation* is not generalized.  More than one *SCN* might be used in a project.  For example, the [Arrowgrams](https://github.com/bmfbp/bmfbp) project contains an SCN for PROLOG-like fact (triple) matching, another SCN for [parsing](https://github.com/guitarvydas/parsing-assembler), another SCN for [scanning](https://github.com/guitarvydas/scanner) (lexing), another SCN for inter-component message passing [cl-event-passing](https://github.com/guitarvydas/cl-event-passing), another SCN for [type definition](https://github.com/guitarvydas/stack-dsl), etc, etc.[^lisp]

[^lisp]: most of the SCNs in Arrowgrams were built on top of Common Lisp and the ESRAP (PEG) parsing library and Lisp macros.  Arrowgrams was a bootstrap project.  Since then, I discovered Ohm-JS and, maybe, would have used it instead of some of the other technologies.  This was a chicken-before-the-egg problem: we had to use _something_ to implement the bootstrapped version.

[DSL means Domain Specific Language, GPL means General purpose Programming Language].

# Example

I'm working on this at the moment, it is unfinished and not debugged, but gives some of the flavor of what a DSL for DI might be:

```
# types
  rid = {
    path
    ns
    name
  }

  thing = compound { val component }

  val = any

  component = :foreign
  parent-component = component
  child = component

  any = :foreign

  string = :foreign
  path = :foreign
  ns = :foreign
  name = :foreign

  yesno = 'yes' | 'no'
  
# end types

# signatures

// RID means Relative ID
def-component% <rid
def-input% <rid
def-output% <rid
get% <rid >val
set% <rid <val

# layer effective address
// ea means Effective Address - the resolved path part of a RID
ea% <path >component
def-ea% <path >component
# end layer effective address

# end signatures

# foreign functions
// foreign functions are defined elsewhere (in the base language)
// synchronous and always return a value
is leaf <rid >yesno
lookup component at top level <path <ns <name >component
lookup contained component <path <ns <name >component
lookup or create component at top level <path <ns <name >component
lookup or create contained component <path <ns <name >component
create input pin raw <path <ns <name
create output pin raw <path <ns <name
raw get <parent <rid.ns <rid.name
raw set <parent <rid.ns <rid.name <v
# end foreign functions

# implementation

def-top-level-component% <name
  component = @lookup or create component at top level <name
  component

def-contained-component% <rid
  outer = def-ea% <rid.path
    design rule `must use component namespace' <rid
  component = @lookup or create contained component <path.path <path.ns <path.name
  component

def-input% <rid
  outer = ea% <rid.path
    design rule `must use input namespace' <rid
    design rule `input pin must not be defined more than once` <outer <rid.ns <rid.name
  @create-input-pin-raw <outer <rid.ns <rid.name
  nothing   

def-output% <rid
  outer = ea% <rid.path
    design rule `must use output namespace' <path
    design rule `output pin must not be defined more than once` <outer <rid.ns <rid.name
  @create-output-pin-raw <out <rid.ns <rid.name
  nothing   

get% <rid >val
  parent = ea% <rid.path
    design rule `must be a valid namespace' <rid
    design rule `value must exist' <parent <rid.ns <rid.name
  v = @raw-get <parent <rid.ns <rid.name
  v
   
set% <rid <val
  parent = ea% <rid.path
    design rule `must be a valid namespace' <rid
    design rule `value must not exist' <parent <rid.ns <rid.name
  @raw-set <parent <rid.ns <rid.name <v
  nothing   

add-connection% <rid <rid1 <rid1
  parent = ea% <rid.path
    design rule `must use connection namespace' <rid
    design rule `must use i/o namespace' <rid1
    design rule `must use i/o namespace' <rid2
  @raw-add-connection <rid.name <parent <rid1 <rid2

# layer `effective address'
ea% <path >component
    design rule `must use component namespace' <path.ns
  [ @is leaf <path
    yes -> component = @lookup component at top level <path
    no  ->
      outer = ea% <path.path
        design rule `must be a component' <outer
        design rule `value must exist' <outer <path.ns <path.name
      component = @lookup contained component <outer <path.ns <path.name
  ]
  component


def-ea% <path >component
  [ @is leaf <path.path
    yes -> component = @lookup or create component at top level <path.path <path.ns <path.name
    no  ->
      outer = ea% <path.path
      component = @lookup or create contained component <outer <path.ns <path.name
  ]
  component
# end layer `effective address'


# end implementation

# design rules
`must use component namespace' <rid
`must use input namespace' <rid
`must use output namespace' <rid
`input pin must not be defined more than once` <component <ns <name
`output pin must not be defined more than once` <component <ns <name
`must be a valid namespace' <rid
`value must exist' <path <ns <name
`value must not exist' <path <ns <name
`must be a component' <any
`must use connection namespace' <rid
`must use i/o namespace' <rid
# end design rules

```

This is an expression language - everything returns a value.  Statements are processed in sequence and the value is the last statement encountered.

"#" is used to distinguish sections

Long names that include spaces are written `...' (syntax borrowed from M4).

"<" means input.

">" means output.

Indentation denotes layering.

"@" means call a foreign function (synchronous call).

Foreign functions are implemented elsewhere in some other language.  Akin to *imports* in some languages.

"[]" means *choice* (if-then-else or case).  The first item after "[" is an expression that produces a value that is cased-on.

"x -> ..." means "case x".

The type DSL is documented elsewhere [Type SCN](https://guitarvydas.github.io/2021/07/05/Type-DSL-(SCN).html).

Note that design-rules are relegated to lower levels (deeper indentation). Design rules are like error checks and type checks, but specific to the project-at-hand.  Using current GPLs, these checks would be wound into the code.  It is *possible* to separate design-rule checks from code in current GPLs, but this is not frequently done.

Note that using an *SCN* does <u>not</u> make the logic a no-brainer to understand.  The goal is simply to unwind architecture-thinking from details-thinking.  At present, code maintainers must understand the code they are working on, anyway. This costs time. Splitting the code into DI (Architecture) and Implementation should reduce the effort required to understand a project (but may not save time - understanding still requires thought).  Using an SCN enables higher-level thinking for the architect(s) of a project.

# Layers

Building a project in layers, e.g. using an SCN, enables the stratification of the development process.

An *architect* can write out a design in DI, an *implementation engineer* can work out the details, a *test engineer* can examine the project from a testability perspective, a *coder* can implement the code, etc., etc.  

# Software Development Roles

Further discussion of a protoype set of [roles](https://guitarvydas.github.io/2020/12/10/Software-Development-Roles.html) and stratification of the software development process.

# See Also

[Blog](https://guitarvydas.github.io)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
