---
layout: post
title:  "Elements of a DI Drawing (WIP)"
---

A drawing contains nothing but graphical elements:

- rectangle
- ellipse
- line
- text.

Each element contains:
- `(x,y)` coordinate of centre point

Rectangle contains:
- `(x,y)` coordinate of centre point 
- `(0,0)` is that the top-left of the canvas
- `(w,h)` width and height of rectangle (e.g. top = x-w/2, bottom = x+w/2)
- shape attributes

Ellipse contains:
- `(x,y)` coordinate of centre point 
- `(0,0)` is that the top-left of the canvas
- `(w,h)` width and height of ellipse
- shape attributes

Line contains:
- `(x1,y1)` start point
- `(x2,y2)` end point
- path points `(x,y)`'s excluding `(x1,y1)` and `(x2,y2)`
- line attributes

Text contains:
- `(x,y)` of top-left corner
- attributes
- text attributes

Attributes:
- color

Shape Attributes
- Attributes
- thickness (outline thickness, default=1)

Line attributes

Text Attributes
- Attributes

# DI
DI means Design Intent (often called Architecture)

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
