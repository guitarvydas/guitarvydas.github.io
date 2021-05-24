---
layout: post
title:  "Diagram Notation"
---
This note contains the conventions I use when creating Software Components with Draw.io.

## port
- rectangle that does not include other objects  
- rectangle that can include color, text, strokeWidth
- or, circle

## external port
  port
  circle
  
## internal port
  port
  rect

## input port
  color=green

## output port
  color=yellow or color=red

## explicit port

## implicit port

## component
- rectangle that includes ports, arrows, attributes
- or, ellipse

## link component
  component that only contains attributes, text, ports
### foreign or link?
   link components are components that are not implemented on the given diagram

   link components can be 
   1. implemented by other diagrams, or, 
   2. directly implemented in the base language
   
Link components used to be called Leaf components.  

Link is a general concept - we cannot know how the component will be implemented.  

All links must be resolved before running a Component hierarchy.

Links can be resolved incrementally.  For example, Component A can be joined to Component B, which results in hierarchical system C that might contain unresolved links.

## composite component
  component that contains other objects

# See Also

https://guitarvydas.github.io/2021/01/14/References.html
https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
