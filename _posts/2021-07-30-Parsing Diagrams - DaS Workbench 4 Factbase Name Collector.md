---
layout: post
title:  "Parsing Diagrams - DaS Workbench 4 Factbase Name Collector"
---

# Name Collector

We are just about ready to emit code for the diagram and we could immediately do so if we used Drawio's ids.

Drawio creates unique ids for mxCell elements, but they are long and not very readable.

We want to use much shorter ids, at least during debugging and bootstrapping[^1].

[^1]: The Drawio ids are OK, as long as we don't need to look at them.

We can invent ids very simply when we encounter new mxCell nodes, but we run into trouble with forward references.  For example, `source` and `target` cells refer to ids of other nodes.  In some cases, the referenced cells have not yet been encountered (in a top-to-bottom traversal of the mxGraph structure.)

Drawio has already handled this problem, so this is just a bit of accidental complexity that we have created for ourselves.

There are many ways to solve this problem, e.g. invent ids as soon as we see a reference and then remember to use that same id instead of inventing one when we encounter the mxCell definition.

Most of these techniques involve tricks and extra code.

The *most straightforward* way to deal with this problem is to invent names first, then emit code, in other words create code in two passes:

1. invent and collect names
2. emit code.

[_Aside: most modern GPLs avoid this problem by insisting on declaration-before-use_.]

We will lean on the pattern matcher, again, and insert a simple phase into our workflow that simply invents and collects ids, but doesn't emit any code.

### Forward References

The purpose of this phase is to walk the input, emit nothing, but build up a table of names which can be used in the following phase.  

[_Assemblers tend to work this way.  They are often written as two passes.  The first pass picks up all of the labels in code, and the second pass emits the required binary instructions_.]

### Obfuscation

Aside: most programmers would attempt to insert the name collection code into one of the preceding passes.  

This is an optimization. 

This would obfuscate the code in the previous passes. 

Even worse, this kind of optimization is usually done manually.  

If this really becomes a problem (an efficiency issue), then we should want to maintain separation of concerns.  

We would want to write the the code as two separate phases, then join the phases together into a single piece of code using a script.

In some ways, the use of declaration-before-use has blinded the programming community to building code in layers and using automation to weave layers together.

# Forward Reference Name Collector

![2021-07-30 to fb 1.png](https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-07-30%20to%20fb%201.png?raw=true)

## Grok

The grok grammar follows

```
Tofb1{
  Diagrams = Diagram+
  Diagram = "<diagram" Attribute* ">" GraphModel "</diagram>"
  Attribute = NameAttribute | DiagramIDAttribute | OtherAttribute
  NameAttribute = "name" "=" string
  DiagramIDAttribute = "id" "=" string
  OtherAttribute = alnum+ "=" attributeValue
  string= "\"" notDQ* "\""
  notDQ = ~"\"" any
  attributeValue = number | string
  number = digit+

  GraphModel = "<mxGraphModel" Attribute+ ">" Root "</mxGraphModel>" 
  Root = "<root>" Cell+ "</root>"
  Cell = CellWithContent | CellWithoutContent
  CellWithoutContent = "<mxCell" CellAttribute+ "/>"
  CellWithContent = "<mxCell" CellAttribute+ ">" Geometry? "</mxCell>"	     
  Geometry = "<mxGeometry" GAttribute+ "/>"
CellAttribute =     EllipseAttribute
                  | TextAttribute 
                  | KindAttribute 
                  | ValueAttribute 
		  | EdgeAttribute
		  | VertexAttribute
		  | SourceAttribute
		  | TargetAttribute
		  | IDAttribute
		  | RedAttribute
		  | OtherCellAttribute
  EllipseAttribute = "kind" "=" quote "ellipse" quote
  TextAttribute = "kind" "=" quote "text" quote
  KindAttribute = "kind" "=" string
  ValueAttribute = "value" "=" string
  SourceAttribute = "source" "=" string
  TargetAttribute = "target" "=" string
  IDAttribute = "id" "=" string
  EdgeAttribute = "edge" "=" quote "1" quote
  VertexAttribute = "vertex" "=" quote "1" quote
  RedAttribute = "fillColor" "=" quote "red" quote
  OtherCellAttribute = alnum+ "=" attributeValue

  GAttribute =   ASGAttribute
               | RelativeGAttribute 
               | OtherGAttribute 
  ASGAttribute = "as" "=" string
  RelativeGAttribute = "relative" "=" string
  OtherGAttribute = alnum+ "=" attributeValue

  quote = "\""
}

```

The work is done in the emit code:

## Emit

```
Diagrams [@ds] = {{ resetNames (); }}[[${nameMangle (ds)}]]
Diagram [k @a k2 graphmodel k3] = {{ scopeAdd ('diagramid', '') }}[[${a}${graphmodel}]]
Attribute [a] = [[${a}]]
NameAttribute [an k s] = [[]]
DiagramIDAttribute [an k s] = [[${newDiagramID (s)}\n${getDiagramID()}\t\t${s}\n]]
OtherAttribute [@an k s] = [[\ ${an}${k}${s}]]
string [q1 @cs q2] = [[${q1}${cs}${q2}]]
notDQ [c] = [[${c}]]
attributeValue [x] = [[${x}]]
number [n] = [[${n}]]

GraphModel [k1 @as k2 root k3] = [[${root}]]
Root [k1 @cells k2] = [[${cells}]]
Cell [c] = {{scopeAdd ('cellid', '');}}[[${c}]]
CellWithoutContent [k1 @as k2] = [[${as}]]
CellWithContent [k1 @as k2 @geometry k3] = [[${as}${geometry}]]
Geometry [k1 @as k2] = [[${as}]]

CellAttribute [a] = [[${a}]]
EllipseAttribute [kind eq q1 s q2] = [[]]
TextAttribute [kind eq q1 s q2] = [[]]
KindAttribute [kind eq s] = [[]]
ValueAttribute [v eq s] = [[]]
SourceAttribute [v eq s] = [[]]
TargetAttribute [v eq s] = [[]]
IDAttribute [id eq s] = [[${newCellID(s)}${getCellID()}\t\t${s}\n]]
EdgeAttribute [v eq q1 s q2] = [[]]
VertexAttribute [v eq q1 s q2] = [[]]
RedAttribute [id k q1 s q2] = [[]]
OtherCellAttribute [@an k s] = [[]]

GAttribute [a] = [[${a}]]
ASGAttribute [kas k s] = [[]]
RelativeGAttribute [r k s] = [[]]
OtherGAttribute [@an k s] = [[]]

quote [c] = [[${c}]]

```



The name invention and collection work is done in the `newDiagramID()` and `newCellID()` functions.

The calls to `getDiagramID()` and `getCellID()` are theoretically unneccessary, but help in pretty-printing the name table at the the end of the pass.

This phase emits "nothing".  

It creates a table which is made available to the next phase.

To aid debugging, the table is dumped at the end of this phase, resulting in the following output in the textarea marked as "diagrams to net fb1:" (labelled 'tofb1transpiled').

```

id1		"kCBzqsQgc0aW30EmMs_m"
id2		"0"
id3		"1"
id4		"Nl1LcCOVLVZGkuQ6EcLl__2"
id5		"Nl1LcCOVLVZGkuQ6EcLl__3"
id6		"Nl1LcCOVLVZGkuQ6EcLl__4"
id7		"JY7Yr9pDnzS2nqslWDs0__1"
id8		"Nl1LcCOVLVZGkuQ6EcLl__6"
id9		"Nl1LcCOVLVZGkuQ6EcLl__7"
id10		"JY7Yr9pDnzS2nqslWDs0__2"
id11		"Nl1LcCOVLVZGkuQ6EcLl__9"
```



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
