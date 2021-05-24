---
layout: post
title:  "Software Components 101 - Part 13 Identity Grammar Before Creating a Factbase"
---
# Introduction
We create a factbase from the nested documents created in previous essays.

## Identity Grammar
```
BRACES2FB {
  topLevel = ws+ tBEGIN rect tEND


  nestedAttributesOrObjects = tBEGIN attributeOrObject+ tEND
  attributeOrObject = attribute | object

  object = rect | ellipse | circle | arrow
  rect = tRECT synonym nestedAttributesOrObjects? ws*
  circle = tCIRCLE synonym nestedAttributesOrObjects? ws*
  ellipse = tELLIPSE synonym nestedAttributesOrObjects? ws*
  arrow = tARROW sender receiver ws*

  attribute = shapeAttribute | colorAttribute | strokeWidthAttribute
  shapeAttribute = "shape" ws* "rounded" ws*
  colorAttribute = "color" ws* color ws*
  strokeWidthAttribute = "stroke-width" ws* number ws*

  sender = qualident ws*
  receiver = qualident ws*

  synonym = qualident ws*

    /* mid-level */
    tRECT = "rect" ws*
    tCIRCLE = "circle" ws*
    tELLIPSE = "ellipse" ws*
    tARROW = "arrow" ws*

    tBEGIN = "{" ws*
    tEND = "}" ws*

      /* low-level */
      color = rgba | "green" | "yellow" | "red"

      keyword = color

      flat_ident = ~keyword flat_ident_char+ 
      flat_ident_char = "a" .. "z"
      qualident = qualident_recursive | flat_ident
      qualident_recursive = flat_ident "/" qualident

      number = dig+
      dig = "0" .. "9"
      rgba = hex hex hex hex
      hex = hd hd
      hd = dig | "A" .. "F"
 
      ws = " " | "\t" | newline
      newline = "\n"
}



  topLevel [@ws begin rect end] = [[${ws}${begin}${rect}${end}]]


  nestedAttributesOrObjects [begin @aorobj end] = [[${begin}${aorobj}${end}]]
  attributeOrObject [aorobj] = [[${aorobj}]]

  object [obj] = [[${obj}]]
  rect [rect syn @nested @ws] = [[${rect}${syn}${nested}${ws}]]
  circle [circle syn @nested @ws] = [[${circle}${syn}${nested}${ws}]]
  ellipse [ellipse syn @nested @ws] = [[${ellipse}${syn}${nested}${ws}]]
  arrow [arrow sender receiver @ws] = [[${arrow}${sender}${receiver}${ws}]]

  attribute [attr] = [[${attr}]]
  shapeAttribute [shape @ws1 rounded @ws2] = [[${shape}${ws1}${rounded}${ws2}]]
  colorAttribute [k @ws1 color @ws2] = [[${k}${ws1}${color}${ws2}]]
  strokeWidthAttribute [sw @ws1 n @ws2] = [[${sw}${ws1}${n}${ws2}]]

  sender [ident @ws] = [[${ident}${ws}]]
  receiver [ident @ws] = [[${ident}${ws}]]

  synonym [ident @ws] = [[${ident}${ws}]]

    tRECT [t @ws] = [[${t}${ws}]]
    tCIRCLE [t @ws] = [[${t}${ws}]]
    tELLIPSE [t @ws] = [[${t}${ws}]]
    tARROW [t @ws] = [[${t}${ws}]]

    tBEGIN [t @ws] = [[${t}${ws}]]
    tEND [t @ws] = [[${t}${ws}]]

      color [cl] = [[${cl}]]

      keyword [kw] = [[${kw}]]

      flat_ident [@cs] = [[${cs}]]
      flat_ident_char [c] = [[${c}]]
      qualident [ident] = [[${ident}]]
      qualident_recursive [flatident slash recursiveident] = [[${flatident}${slash}${recursiveident}]]

      number [num] = [[${num}]]
      dig [digit] = [[${digit}]]
      rgba [h1 h2 h3 h4] = [[${h1}${h2}${h3}${h4}]]
      hex [h1 h2] = [[${h1}${h2}]]
      hd [c] = [[${c}]]
 
      ws [c] = [[${c}]]
      newline [c] = [[${c}]]
```
The identity grammar should produce output that is the same as the input.

Check that `v.fb` is the same as `v.brace`.

Eye-ball or use `diff`.  

Look for low-hanging fruit.

[We can always come back and fix errors, so this doesn't need to be perfect.  The only test will be if the app is good enough for its purposes.  Everything is a fractal, everything is relative, nothing is absolute.  Absolute perfection is not possible.  Trying to attain absolute perfection will retard higher-level learning and progress.  Waterfall design is the process of closing doors behind you, whereas FDD[^fdd] leaves doors open on the assumption that iteration will be needed (design iteration as well as code iteration)].

[^fdd] FDD means Failure Driven Design.

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
