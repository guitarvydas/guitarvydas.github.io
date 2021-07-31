---
layout: post
title:  "Parsing Diagrams - DaS Workbench 1 Decoding Phase"
---

# Goal of DaSWB - Diagrams as Syntax WorkBench

The DaS Workbench ("Diagrams as Syntax Workbench") transpiles a raw .drawio file into code.

In this example, we will use the drawing `final.drawio` and transpile it into PROLOG facts.

# Decoding

Drawio (aka diagrams.net) stores diagrams as compressed XML in `mxFile` format.

The first step of transpiling the .drawio file into code is to uncompress the data.

The uncompression is done automatically, using a bit of JavaScript code.  The support code can be found in support.js. 

The uncompressed code is deposited into the textarea with id ="decodertranspiled" seen below:

![2021-07-30 Decode.png](https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-07-30%20Decode.png?raw=true)

The textarea is currently only 1 line high, but all of the code can be copied (e.g. using ⌘-a, ⌘-c).

Paste the code into an editor and pretty-print it as HTML (convert "<" into newline-"<", then format).

```

<diagram id="kCBzqsQgc0aW30EmMs_m" name="Page-1">

  <mxGraphModel dx="673" dy="353" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1100" pageHeight="850" math="0" shadow="0">
    <root>
      <mxCell id="0"/>
      <mxCell id="1" parent="0"/>
      <mxCell id="Nl1LcCOVLVZGkuQ6EcLl-2" value="m" style="rounded=1;whiteSpace=wrap;html=1;verticalAlign=top;" parent="1" vertex="1">
	<mxGeometry x="120" y="80" width="440" height="210" as="geometry"/>
      </mxCell>
      <mxCell id="Nl1LcCOVLVZGkuQ6EcLl-3" value="n" style="rounded=1;whiteSpace=wrap;html=1;verticalAlign=top;" parent="1" vertex="1">
	<mxGeometry x="180" y="120" width="320" height="140" as="geometry"/>
      </mxCell>
      <mxCell id="Nl1LcCOVLVZGkuQ6EcLl-4" value="b" style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;fillColor=#fff2cc;align=center;strokeColor=#d6b656;textOpacity=50;" parent="1" vertex="1">
	<mxGeometry x="540" y="175" width="30" height="30" as="geometry"/>
      </mxCell>
      <mxCell id="JY7Yr9pDnzS2nqslWDs0-1" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" edge="1" parent="1" source="Nl1LcCOVLVZGkuQ6EcLl-6" target="Nl1LcCOVLVZGkuQ6EcLl-7">
	<mxGeometry relative="1" as="geometry"/>
      </mxCell>
      <mxCell id="Nl1LcCOVLVZGkuQ6EcLl-6" value="a" style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;fillColor=#d5e8d4;align=center;strokeColor=#82b366;textOpacity=50;" parent="1" vertex="1">
	<mxGeometry x="110" y="175" width="30" height="30" as="geometry"/>
      </mxCell>
      <mxCell id="Nl1LcCOVLVZGkuQ6EcLl-7" value="c" style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;fillColor=#d5e8d4;align=center;strokeColor=#82b366;textOpacity=50;" parent="1" vertex="1">
	<mxGeometry x="174" y="175" width="30" height="30" as="geometry"/>
      </mxCell>
      <mxCell id="JY7Yr9pDnzS2nqslWDs0-2" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;" edge="1" parent="1" source="Nl1LcCOVLVZGkuQ6EcLl-9" target="Nl1LcCOVLVZGkuQ6EcLl-4">
	<mxGeometry relative="1" as="geometry"/>
      </mxCell>
      <mxCell id="Nl1LcCOVLVZGkuQ6EcLl-9" value="d" style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;fillColor=#fff2cc;align=center;strokeColor=#d6b656;textOpacity=50;" parent="1" vertex="1">
	<mxGeometry x="474" y="175" width="30" height="30" as="geometry"/>
      </mxCell>
    </root>
  </mxGraphModel>

</diagram>

```

We see that drawio saves each diagram element as an `mxCell` element with a unique (albeit unmemorable) id.

## Grok and Emit

Transpiling the .drawio file consists of repeatedly applying a 2-step process:

1. **Grok** - understand the input.  
2. **Emit** - rearrange the input into some other format.

Grok is pattern-matching. Formally, this is known as *parsing*. At the time of writing, PEG parsers seem to be the easiest parsers to build and use. We happen to use a PEG library called Ohm-JS.

The Emit phase just outputs the matched code, possibly rearranged and embellished. We happen to use JS "template" (backtick) strings, which form the basis of the *glue* tool.  

Ohm-JS performs the *grok* phase using a REGEXP-like syntax[^syntax].

[^syntax]: If you don't already know REGEXP syntax, skip it and go directly to learning PEG syntax.  You probably don't even need to know PEG syntax to read the rest of these artcles.

Ohm-JS leaves the *emit* phase up to the programmer. In this case, we've written a simplistic tool, called *glue*, that generates JS template strings from a specification.

### Grok

For the decompressor, the *grok* code is quite simple:

- it pattern-matches an mxfile header, 
- then matches one or more compressed diagrams, 
- then matches a trailer.

The actual code for grok is an Ohm-JS grammar.

You can see this code by copying the code from the textarea labelled "grok (decoder)".  For discussion, the code appears below:

![2021-07-30 grok decoder.png](https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-07-30%20grok%20decoder.png?raw=true)



```
AppDiagramsEncodedNet{
  TabbedDiagrams = Header Diagram+ Trailer
  Header = "<" "mxfile" encodedChar+
  Trailer = "</mxfile>"
  Diagram = "<diagram" Attribute* ">" encodedChar+ "</diagram>"
  Attribute = alnum+ "=" attributeValue
  string= "\"" notDQ* "\""
  notDQ = ~"\"" any
  encodedChar = ~"<" any		   
  attributeValue = number | string
  number = digit+
}

```

Ohm-JS grammars are based on PEG grammars.  The syntax is very similar to REGEXP, except that matches are arranged in *rules* and *rules* can call one another.

The above says:

- The pattern-matcher (grok grammar) is named "AppDiagramEncodedNet"
- The block of pattern matching rules is eclosed in brace brackets {}
- Example: the *rule* named "TabbedDiagrams" consists of calls to 3 other rules:
  - Header
  - Diagram
  - Trailer
- The Header and Trailer rules must match *exactly* once.
- The *rule* Diagram is to be matched one or more times (specified by the `+` operator). 
- An equals sign `=` separates the rule name from the rule body.
- The other rules are similar
  - `"..."` matches a literal string
  - `*` matches zero or more times
  - `|` specifies alternation, e.g. `(A | B) means to match an A or a B
- Note that rule names are case-sensitive
- Note that rules with names beginning with capital letters work differently than rules with lower-case first-letter names in Ohm-JS
  - Capitalized rules skip spaces
  - Non-capitalized rules do not skip spaces (the default for most other PEG libraries).
- `Any` is a special operator in Ohm-JS, meaning to match any single character.
- `~` is an Ohm-JS operator that succeeds only if the immediately subsequent pattern fails, e.g. `~"\\"" any` means to match one character that isn't a double-quote
- Backslashes are used to escape certain characters
- Further details about Ohm-JS syntax is found in the Ohm-JS documentation. 

### Emit

Likewise, we can examine the emit code by copying the "emit (decoder):" textarea and viewing it.

![2021-07-30 emit decoder.png](https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-07-30%20emit%20decoder.png?raw=true)



```
TabbedDiagrams [h @d t] = [[${d}]]
Header [k k2 @ec] = [[${k}${k2}${ec}]]
Trailer [k] = [[${k}]]
Diagram [k @a k2 @ec k3] = [[${k}${a}${k2}\n${decodeMxDiagram(ec)}\n${k3}\n]]
Attribute [@an k s] = [[\ ${an}${k}${s}]]
string [q1 @cs q2] = [[${q1}${cs}${q2}]]
notDQ [c] = [[${c}]]
encodedChar [c] = [[${c}]]
attributeValue[x] = [[${x}]]
number [n] = [[${n}]]

```

The above code is arranged as rules, with *exactly* the same names as the pattern matching rules.

After pattern matching has finished (and succeeded), the above rules are called to emit code for each match.  

The right-hand side of the rules contain

1. a rule name
2. a list of parameters to the rule - essentially variables corresponding to each match ; the `@` symbol means that the grammar contained one of the operators `?`, `*` or `+` for a given match[^param].

The left-hand side of the rules contain rewriting commands in the form of JS template strings surrounded by double-brackets `[[]]`.

[^param]: unlike parameters in most languages, it is possible to use operators in the parameter list (this choice was inspired by relational programming)

For example, the first rule `TabbedDiagrams` expects 3 matches and assigns them to the variables `h, d and t`.  The second parameter matches 1-or-more times (using the `+` operator in the grok grammar).  The first rule returns the value of the `d` parameter and ignores the `h and t` parameters.  The `d` parameter is created recursively from the subsequent rules and matches[^@].

[^@]: The "@" parameter operator signifies recursive deconstruction of the parameter `d`.

The aim of this first rule is to return the *diagram* portion of the source text and to drop the header and trailers from the source.

The other *emit* rules work in a similar fashion.

The goal of this grok/emit phase is *only* to recognize incoming .drawio files and to break them up into headers and diagrams.  More interesting manipulations of the incoming .drawio files remains the domain of subsequent phases.

The syntax for these rules is further described in the glue manual.

# Next

After decompressing the .drawio file, we'll perform a few cleanups, then convert the code into PROLOG.

It is possible to convert the code into just about any GPL, not just PROLOG.  PROLOG was chosen because it has a fairly clean syntax for representing triples.  Triples can be reprented as Lisp sexps, or user-defined data structures, etc.

We will not go into as much syntactic detail in subsequent articles.

# See Also

[daswb.html](https://github.com/guitarvydas/diagram-parsing/blob/master/daswb.html)

[drawio / diagrams.net](https://www.diagrams.net)

[Ohm-JS source and documentation](https://github.com/harc/ohm)

[Glue Tool](https://guitarvydas.github.io/2021/04/11/Glue-Tool.html)

[Glue Manual](https://guitarvydas.github.io/2021/03/24/Glue-Manual.html)

[Blog](https://guitarvydas.github.io)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
