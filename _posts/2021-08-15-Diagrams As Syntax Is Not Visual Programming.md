---
layout: post
title:  "Diagrams As Syntax Is Not Visual Programming"
---

# DaS
DaS means Diagrams as Syntax.


# DaS Is Not Textual Programming
DaS Is Not Textual Programming

# DaS Is Not Visual Programming
DaS Is Not Visual Programming

# DaS Is A Hybrid

There is a gap between textual and visual programming.

DaS sits in that gap.

DaS is a hybrid - diagrams + text.

In DaS, we do not consider pixels.

# Primitive DaS Objects
- rectangles
- ellipses
- text
- lines.

Every object has an (x,y) coordinate.

Objects can overlap.

# Comparison To Textual Programming

In textual programming, using text editors, the basic object (the basic unit) is the _character_.

In textual programming, _characters_ do not overlap.

In textual programming, _characters_ have _(line,offset)_ grid positions instead of _(x,y)_ positions that may overlap.

# SVG

SVG already contains the basics needed to create DaS editors, i.e. rectangles, ellipses, text and lines.

Most people use SVG to create complex visual drawings.

For DaS, we need only a small subset of SVG and simple editors.

Currently, I use https://www.diagrams.net for drawings and compile the .drawio format directly into factbases, e.g. https://github.com/guitarvydas/diagrams-as-syntax.

# Ignore Attributes

Most drawings contain a lot of graphical details (e.g. polylines, fonts, stroke-width, etc.).

Most of these can be ignored.

I pick off only the "interesting" bits for DaS, e.g. rectangles, ellipses, text and lines and retain some graphical attributes.


# Inferencing

Inferencing can be used to compile diagrams to code.

Often grade-school math is enough.

## Inclusion

How do you tell if a box is inside another box?

Grade-school math.  (Compare x's and y's).

## Intersection

How do you tell if a graphical object intersects another graphical object?

Grade-school math.  Intersection (made easier if all lines are vertical and horizontal).

## Bounding Boxes

How do you tell if an ellipse intersects a rectangle?

Create bounding boxes for both, then apply grade-school math.

## Bounding Boxes for Lines

Don't do this.

From the transpiler's perspective, we only need to know where the line starts and where it ends.

The gnarly details are handled by the editor, but are not needed by the transpiler.

How do we know where a line starts and ends? Use its _(x,y)_ start and end points, apply grade-school math (intersection). Some editors (like Drawio) give you from/to information, so, in some cases you don't even need to calculate this information.

# Examples
## Box and Arrow

Box-and-arrow diagrams use rectangles, text and lines.

I use circles to represent ports situated on boxes.

I use color="green" for input ports.

I use color="yellow" for output ports.

I use stroke-width=3 for composite components. In most cases, I don't wish to specify how a component is implemented (composite or leaf) on a diagram, so I usually ignore stroke-width.

## Statecharts

Harel's Statecharts use ellipses, text and lines.

# See Also

[StateCharts](https://guitarvydas.github.io/2020/12/09/StateCharts.html)
[StateCharts Again](https://guitarvydas.github.io/2021/02/25/statecharts-(again).html)

[Blog](https://guitarvydas.github.io)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
