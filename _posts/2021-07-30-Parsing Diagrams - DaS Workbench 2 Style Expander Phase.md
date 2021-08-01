---
layout: post
title:  "Parsing Diagrams - DaS Workbench 2 Style Expander Phase"
---

The goal of the style-expander phase is to convert HTML `style` attributes from:

```
style="rounded=1;whiteSpace=wrap;html=1;verticalAlign=top;"
```

to

```
 rounded="1" whiteSpace="wrap" html="1" verticalAlign="top"
```

[_This is probably not legal HTML code, but is useful for later phases. It is OK to produce illegal HTML at this point, as long as subsequent phases can *grok* it._]

This conversion can probably be done in any other programming language, but I chose to do this using *grok* and *emit* (based on Ohm-JS).

It is considered to be better style to create "structured" pattern matches, using a PEG parser engine, than to write the pattern matches in ad-hoc code.

Note that FP languages use pattern matching. PEG parsing is a superset of what is currently available in popular FP languages, but the programming style should be familiar to anyone already using pattern-matching FP languages.

# Style Expansion in DasWB

The pertinent textareas are highlighted below

![2021-07-30 screendshot style expander.png](https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-07-30%20screendshot%20style%20expander.png?raw=true)

We can view the output, as before, by copying the text area "diagrams net style expanded"[^1] and dropping it into a text editor.

[^1]: id="styleexpandertranspiled"

## Grok

```
AppStyleexpander{
  Diagrams = Diagram+
  Diagram = "<diagram" Attribute* ">" GraphModel "</diagram>"
  Attribute = alnum+ "=" attributeValue
  string= "\"" notDQ* "\""
  notDQ = ~"\"" any
  encodedChar = ~"<" any		   

  GraphModel = "<mxGraphModel" Attribute+ ">" Root "</mxGraphModel>" 
  Root = "<root>" Cell+ "</root>"
  Cell = CellWithContent | CellWithoutContent
  CellWithoutContent = "<mxCell" CellAttribute+ "/>"
  CellWithContent = "<mxCell" CellAttribute+ ">" Geometry? "</mxCell>"	     
  Geometry = "<mxGeometry" Attribute+ "/>"
  CellAttribute = StyleAttribute | OtherCellAttribute
  StyleAttribute = "style" "=" string
  OtherCellAttribute = alnum+ "=" attributeValue

  attributeValue = number | string
  number = digit+

}

```

The grok pattern matcher (grammar) looks at the decompressed version of the .drawio file and includes a bit more detail than before.

Here, we match diagrams and break them down into `GraphModel` and `Cell`s.

The`style` attribute can only occur[^style] in `Cell`s.  Such attributes are deconstructed by the rule `StyleAttribute`.

[^style]: We assume that we are starting with valid HTML code produced by drawio.  We *could* add more design rule checking to validate input, if necessary.  A feature of the this method is that error checking does not need to be wound into the code.  Error checks can be plugged into the workflow as pre-filters.  The code remains understandable and the error checks remain understandable.  Components are *not* abstracted to allow for any kind of input - the Architect ensures that error checks are plugged into the workflow as required by the problem/solution.  Design rule checking (aka error checking) components are pluggable components, like everything else.

## Emit

Again, the emit rules match the grok rules 1:1.

The only job of this phase is to latch onto `style` attributes and to process them using the `expandStyle()` [^2]function.

[^2]:ExpandStyle() can be found in `support.js`.

Note that we are using the pattern matcher to help us identify `style` attributes embedded in `mxCell`s.  Everything else is matched, but is emitted verbatim.

Again, the task of this phase is very small.  The goal is to do one thing well, eschew dependencies, then put it into our workflow and forget about it (build and forget). Nothing we do in subsequent phases should affect the operation of this code[^3].

[^3]: This is a place where hidden dependencies must be eschewed.  For example, Call/Return creates hidden dependencies, which means that we should not use libraries based on Call/Return (i.e. just about any code library).  In this particular case, we write out our results and augment `fb.pl` between phases.  The phases of DaSWB cannot CALL each other, but, we can make a pipeline of isolated phases, joining them together with the file `fb.pl`. (Other techniques for isolation could be used, but are unnecessary at this point. (N.B. most GPLs, like Python, Rust, JS, etc. make it difficult to achieve true isolation (because of the use of CALL/RETURN) without using intermediate files.)).

```
Diagrams [@ds] = [[${ds}]]
Diagram [k @a k2 graphmodel k3] = [[${k}${a}${k2}\n${graphmodel}\n${k3}\n]]
Attribute [@an k s] = [[\ ${an}${k}${s}]]
string [q1 @cs q2] = [[${q1}${cs}${q2}]]
notDQ [c] = [[${c}]]
encodedChar [c] = [[${c}]]

GraphModel [k1 @as k2 root k3] = [[${k1}${as}${k2}${root}${k3}]]
Root [k1 @cells k2] = [[${k1}${cells}${k2}]]
Cell [c] = [[${c}]]
CellWithoutContent [k1 @as k2] = [[${k1}${as}${k2}]]
CellWithContent [k1 @as k2 @geometry k3] = [[${k1}${as}${k2}${geometry}${k3}]]
Geometry [k1 @as k2] = [[${k1}${as}${k2}]]

CellAttribute [a] = [[\ ${a}]]
StyleAttribute [id k s] = [[\ ${expandStyle(s)}]]
OtherCellAttribute [@an k s] = [[\ ${an}${k}${s}]]

attributeValue [x] = [[${x}]]
number [n] = [[${n}]]
```

As can be seen by examing the code, above, `emit` does almost nothing in this case and produces an identity transform (i.e. output == input).

In the single case where a `StyleAttribute` is found, we process the attribute by calling `expandStyle()` and return the resulting string (which should be a string of single attribute/value pairs).

`Emit` simply builds a string.  It glues together matched bits of patterns and returns a single string as the result. DasWB pokes this string into the appropriate textarea.

# See Also

[daswb.html](https://github.com/guitarvydas/diagram-parsing/blob/master/daswb.html)

[Blog](https://guitarvydas.github.io)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
