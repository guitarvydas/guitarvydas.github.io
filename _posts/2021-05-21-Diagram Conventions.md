---
layout: post
title:  "Diagram Conventions"
---

- diagrams consist of boxes (rects), circles (ellipses), arrows, text
- diagram objects - boxes and circles - can contain diagram elements, e.g. other boxes, circles, arrows, text
- arrows (lines) cannot cross object boundaries
- arrows must begin at a rectangle and end at rectangle
- more than one arrow can begin at the same rectangle
- more than one arrow can end at the same rectangle
- diagram objects - boxes and circles - can have color attributes
- diagram objects - boxes and circles - can have stroke-width attributes
- circles that touch the edge of another object - boxes and circles - are considered to be contained within the other object
- rectangles that touch the edge of another object - boxes and circles - are considered to be contained within the other object

The Editor creates facts about the above drawings and leaves the facts in a factbase.

In the best of all worlds, the Editor is automated (e.g. an SVG editor).

In the worst of all worlds, the Editor is a human (e.g. transcribe Draw.io drawings into Cloud Outliner in a human-readable sytanx, then converted (e.g. Ohm-JS) into a factbase.

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
