---
layout: post
title:  "Names and Data Descriptors [Working Paper]"
---
## Kind of Variables
There are three (4) kinds[^kinds] of variables:
1. inherited variables
2. own variables
3. bound parameters
4. temp variables

Variables are locations that can be bound (set).

[^kinds] Note that current languages concentrate on 3 & 4 and tend to shun 1 & 2.  Lisp alists are much like (1).  JavaScript own variables are much like (2).

```
parent { 
  own variables
  child {
    own variables
	code 
	{
	  parameters
      {
	    temp variables
      }
    }
  }
}
```
## Variable Access Syntax
I suggest a unique syntax for accessing every kind of variable.

Access operators are not overloaded, they mean exactly one thing - always.

This is a very "assembler"-like perspective.

Later, syntactic sugar (e.g. with Ohm-JS) can be applied to make SCNs that don't seem to differentiate (at the syntax level) between the various kinds of variables.

Furthermore, there are "special" symbols, like "Args" which is bound by the system before executing the ė.

Variables can be accessed and bound (dereferenced and written-to).

operation | data descriptor | dd tuple | syntax | comment
--- | ---| --- | --- | ---
create own variable | @$^1$own.0[size] | {1,own,0,size,{"...","...",...}} | own name | 
create temporary variable | @$^1$temp.0[size] | {1,own,0,size,{"...","...",...}} | temp ~name | 
deref own variable | - | - | ?name | None if "name" is not in Own space
set own variable | - | - |name ⇐ No | creates "name" in own space, if not present
deref temp variable | - | - | ?~name | 
deref* own variable | - | - |@name | 
deref Arg[name] | @$^1$Args.0[size] | {1,args,0,size,{"...","...",...}} | ⤶name | 
deref parameter variable | @$^1$params.0[size] | {1,params,0,size,{"...","...",...}} | name{} | 
bind value to a temp | - | - |name ≡ ... | 
bind value to a parameter variable | - | - | name{v} | 

A variable is characterized by a tuple:
- number of indirections
- base area (name)
- index (offset) in the base area
- size (in bytes) of the variable
- a list of synonym names

index and size can be *nothing* if these fields have not yet been assigned

## Bases
- own
- temp
- parameter
- arg
- child (containee)
- net
- component
- input port
- output port
- constant
- symbol
- lambda
- language function (classical f(x,y,z,...)->(p,q,r,...))
- language variable

Nets are simply names in the *net* namespace.  Nets are used in asynchronous (e.g. bare-metal) implementations and can be ignored when the system is hosted on a synchronous language/operating system.

## See Also

[Data Descriptors - a compile-time model of data and addressing](https://dl.acm.org/doi/10.1145/24039.24051)
[OCG](https://books.google.ca/books/about/An_Orthogonal_Model_for_Code_Generation.html?id=X0OaMQEACAAJ&redir_esc=y)

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