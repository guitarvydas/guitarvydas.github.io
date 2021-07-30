---
layout: post
title:  "Parsing Diagrams - Connections"
---

# asdf

asdf

# Diagram

Ports can be connected to one another. 

[_Only ports can be connected._]

![2021-07-30 Connections.png](https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-07-30%20Connections.png?raw=true)

Connections are shown as arrows.

Connections appear in the factbase as 3 facts:

1. A declaration, e.g. `edge(e,'').`
2. A source port, e.g. `source(e,a).`
3. A target port, e.g. `target(e,c).`

# Processing Connections

Edges as defined above need no further processing.

Later, we will tie edges to ports to components.

Drawio produces `edge` facts as `mxCell` nodes of the graph.  We don't need to do much more at this point.



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
