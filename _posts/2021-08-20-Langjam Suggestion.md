---
layout: post
title:  "Langjam Suggestion"
---

# General Challenge
Implement a language for Software Architecture that is based on diagrams that include:
- rectangles
- ellipses
- text
- lines / edges.

(i.e. a subset of SVG).

Hint: Do not implement Recursion and Looping.  Recursion and Looping are Implementation details and should not appear in a Software Architecture diagram.

# Specific Challenge

Transpile the given drawio diagram to bash, grash and as many other languages as possible.

# Info: Diagram Conventions
Boxes are software components.

All software components are asynchronous, except red boxes.

Red boxes are synchronous components.

Circles are ports.

Green circles are input ports.

Yellow circles are output ports.

Ports have names.

Boxes have names.

Names of boxes are qualified, e.g. _parent_/_child_.

Boxes can contain other boxes.

Circles must touch the edge of the box that they belong to.

Diagrams are drawn using [Drawio](https://www.diagrams.net).

Design (DI (Design Intent), Architecture) is primary. Efficiency is secondary.

Boxes communicate only via ports (e.g. no shared memory, etc.).

Boxes may Send() data to a port that is not connected and the data will be dropped (e.g. garbage collected later).

Boxes may have inputs that are not connected. Such inputs never fire.

Boxes have queues for input messages.  Boxes must complete processing one message before grabbing another one.

Call/Return doesn't work for this.  Closures work for this[^threads].

[^threads]: Operating System Threads are big closures in disguise.

# Info: Receiving and Send()ing

Components are asynchronous by default.

Components can only communicate by using Send().

Send() works like messages in a message-passing system.

# Diagram HelloWorld


<img src="https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-08-20-HelloWorld.png?raw=true" alt="2021-08-20-HelloWorld.png" style="zoom:67%;" />

There are 3 components in this diagram:

1. hwapp123 - the top-level app, asynchronous ; 1 input `in`, 1 output `out`
2. hwapp123/hwsub23 - a mid-level app, asynchronous (not strictly necessary, included for fun) ; 1 input `A` and 1 output `B` 
3. hwsub23/hwhello - a synchronous component that calls the command `hello` whenever an input (any input) is received on its input pin `in` ; 1 input `in` 1 output `out` (not actually used in this example)

See the Appendix for how this diagram maps to a *bash* script.

A *Dispatcher* runs the transpiled diagram. In this case, we use the Linux dispatcher and don't really need to worry about creating a _Dispatcher()_ routine.

The flow of data/control is:

1. an input (any line of text) is placed into the pipe attached to hwapp123/in 
2. hwapp123 forwards this input to its child hwapp123/hwsub23/A (the `A` input of component hwapp123/hwsub23)
3. hwsub23 forwards this input to its child hwsub23/hwhello on pin `in`
4. hwhello prints its input on the console and sends some result to its output pin `out`.  In this simple case, it does not Send() anything
5. hwapp123/hwsub23 finishes.  It Sends() nothing.
6. hwapp123 finishes.  It Sends() nothing.

## Raw Drawio File
```
<mxfile host="Electron" modified="2021-08-17T04:03:24.475Z" agent="5.0 (Macintosh; Intel Mac OS X 11_3_1) AppleWebKit/537.36 (KHTML, like Gecko) draw.io/14.6.13 Chrome/89.0.4389.128 Electron/12.0.7 Safari/537.36" etag="iuNCdEX2bBK_Gqinlbdj" version="14.6.13" type="device"><diagram id="YtQpuq6dlgVgQ-RkE8U0" name="HelloWorld">7VlNc5swEP01PiYDkiHiGH+kPaTTmXg6SY8yCFCLESMLg/vrK4H4CsQhEzvxjGMfzK5Wi/TevhUkEzjf5N84TsIfzCPRBBhePoGLCQCmadjyR3n2pefKNMzSE3Dq6ajGsaL/iHYa2ptSj2w7gYKxSNCk63RZHBNXdHyYc5Z1w3wWde+a4ID0HCsXR33vI/VEWG/MaAa+ExqE+tbI0gMbXAVrxzbEHstaLricwDlnTJRXm3xOIoVehUs57+6F0XphnMRizISVM9tZV7PF/YP/OP2VLNDjw/JKZ9nhKNUbDjOcJCaAetFiXyHBWRp7RCUzJ3CWhVSQVYJdNZpJ8qUvFJtID+8IF1SieBvRIJY+wVSAT6NoziLGi4zQt9RX+reCs7+kNWIXHzWDxaLlLz/Sr5ct70LyF/Ewa5RlfRK2IYLvZYieAKaaGF2aCFmlnTU821VM2KK4noh1bQV17gZ+eaEZeAMb4AAbd2G2TdeXwItjX1sdZhyzz4xlDjBjolMxAweY0XRIYkKZgb2PGCZHqFAblg0EzrDmx5WgET6aOOQS1x0ibo2saZH4CARBx3pOUNX0WgRBwxkgyDwVQdM+Qe8nxcPbsI59K0Mb6nnqrseAfGrfdAF3+oCb9gDg0DoR3lYPbxr3wJZ55DlNXgcab5Py8PZprgB/XtieRZA3HUK9V+kIrGHRoiTa4meXs2MUP0LPmADX/e4EB5oTPFXp233cPfkMo03GRcgCFuNo2XhnjQwULk3MPVN9peDkDxFirx/IcCpYlzGSU/HUuv6tUl1b2lrkOnNh7Csjltt9ahutWcpsphVWNa/cn9rUYdIkBizlLjmAlZaRwDwg4tBzERiuAk4iLOiuu5CjM3rTExdLxenU5fs+KI6N19Xl2WvbOp26bATOTV3Ol7pGq6s63V+Vl/WZ6qpW2ZLX7SUcXcDpvvCcgbjqyvpS1wh1gbGHl/2p8uq/xc4u4ey6OT95mfalPkgg++zIAOCr143vdWhsrzOG6+CDeh3qCewyXoNrmXyEvqTZ/Jm8GGv9twEu/wM=</diagram></mxfile>
```
## Uncompressed File

```

```

```
<diagram id="YtQpuq6dlgVgQ-RkE8U0" name="HelloWorld">

  <mxGraphModel dx="1106" dy="-101" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1100" pageHeight="850" math="0" shadow="0">
    <root>
      <mxCell id="0"/>
      <mxCell id="1" parent="0"/>
      <mxCell id="S9Bv5-BDLRfW4UpD8WRE-1" value="hwapp123" style="rounded=1;whiteSpace=wrap;html=1;verticalAlign=top;fillColor=#f5f5f5;strokeColor=#666666;fontColor=#333333;" vertex="1" parent="1">
	<mxGeometry x="240" y="885" width="640" height="240" as="geometry"/>
      </mxCell>
      <mxCell id="S9Bv5-BDLRfW4UpD8WRE-2" value="hwapp123/hwsub23" style="rounded=1;whiteSpace=wrap;html=1;verticalAlign=top;fillColor=#f5f5f5;strokeColor=#666666;fontColor=#333333;" vertex="1" parent="1">
	<mxGeometry x="296.5" y="915" width="510" height="180" as="geometry"/>
      </mxCell>
      <mxCell id="S9Bv5-BDLRfW4UpD8WRE-3" value="hwsub23/hwhello" style="rounded=1;whiteSpace=wrap;html=1;opacity=50;align=center;verticalAlign=top;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="1">
	<mxGeometry x="395.5" y="950" width="309" height="110" as="geometry"/>
      </mxCell>
      <mxCell id="S9Bv5-BDLRfW4UpD8WRE-4" value="hello" style="rounded=1;whiteSpace=wrap;html=1;dashed=1;opacity=50;align=center;verticalAlign=middle;" vertex="1" parent="1">
	<mxGeometry x="467" y="990" width="169" height="35" as="geometry"/>
      </mxCell>
      <mxCell id="S9Bv5-BDLRfW4UpD8WRE-5" value="in" style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;fillColor=#d5e8d4;align=center;strokeColor=#82b366;textOpacity=50;" vertex="1" parent="1">
	<mxGeometry x="388" y="992.5" width="30" height="30" as="geometry"/>
      </mxCell>
      <mxCell id="S9Bv5-BDLRfW4UpD8WRE-6" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" edge="1" parent="1" source="S9Bv5-BDLRfW4UpD8WRE-7" target="S9Bv5-BDLRfW4UpD8WRE-12">
	<mxGeometry relative="1" as="geometry"/>
      </mxCell>
      <mxCell id="S9Bv5-BDLRfW4UpD8WRE-7" value="out" style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;fillColor=#fff2cc;align=center;strokeColor=#d6b656;textOpacity=50;" vertex="1" parent="1">
	<mxGeometry x="682" y="992.5" width="30" height="30" as="geometry"/>
      </mxCell>
      <mxCell id="S9Bv5-BDLRfW4UpD8WRE-9" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" edge="1" parent="1" source="S9Bv5-BDLRfW4UpD8WRE-10" target="S9Bv5-BDLRfW4UpD8WRE-5">
	<mxGeometry relative="1" as="geometry"/>
      </mxCell>
      <mxCell id="S9Bv5-BDLRfW4UpD8WRE-10" value="A" style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;fillColor=#d5e8d4;align=center;strokeColor=#82b366;textOpacity=50;" vertex="1" parent="1">
	<mxGeometry x="290" y="992.5" width="30" height="30" as="geometry"/>
      </mxCell>
      <mxCell id="S9Bv5-BDLRfW4UpD8WRE-21" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" edge="1" parent="1" source="S9Bv5-BDLRfW4UpD8WRE-12" target="S9Bv5-BDLRfW4UpD8WRE-16">
	<mxGeometry relative="1" as="geometry"/>
      </mxCell>
      <mxCell id="S9Bv5-BDLRfW4UpD8WRE-12" value="B" style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;fillColor=#fff2cc;align=center;strokeColor=#d6b656;textOpacity=50;" vertex="1" parent="1">
	<mxGeometry x="790" y="992.5" width="30" height="30" as="geometry"/>
      </mxCell>
      <mxCell id="S9Bv5-BDLRfW4UpD8WRE-16" value="out" style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;fillColor=#fff2cc;align=center;strokeColor=#d6b656;textOpacity=50;" vertex="1" parent="1">
	<mxGeometry x="860" y="992.5" width="30" height="30" as="geometry"/>
      </mxCell>
      <mxCell id="S9Bv5-BDLRfW4UpD8WRE-22" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" edge="1" parent="1" source="S9Bv5-BDLRfW4UpD8WRE-18" target="S9Bv5-BDLRfW4UpD8WRE-10">
	<mxGeometry relative="1" as="geometry"/>
      </mxCell>
      <mxCell id="S9Bv5-BDLRfW4UpD8WRE-18" value="in" style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;fillColor=#d5e8d4;align=center;strokeColor=#82b366;textOpacity=50;" vertex="1" parent="1">
	<mxGeometry x="230" y="992.5" width="30" height="30" as="geometry"/>
      </mxCell>
    </root>
  </mxGraphModel>

</diagram>

```



# Appendix Drawio Uncompressor

```
 function decodeMxDiagram (encoded) {
    var data = window.atob (encoded);
    var inf = pako.inflateRaw (
	     Uint8Array.from (data, c=>c.charCodeAt (0)), {to: 'string'})
    var str = decodeURIComponent (inf);
    return str;
}
```



# Appendix Concurrency (Call / Return Spaghetti)

[Call Return Spaghetti](https://guitarvydas.github.io/2020/12/09/CALL-RETURN-Spaghetti.html)

# Hints

## Bounding Boxes

It is easier to determine containment if you first create a bounding box (left, top, right, bottom) for each graphical object of interest (except lines).

## Grash

[Grash](https://github.com/guitarvydas/vsh/tree/master/grash) (GRAphical SHell) is a small C program (approx. 250 lines) that works like /bin/bash but has most of the features stripped out.  

Grash only creates forks and execs named programs using pipes.

## VSH

A prototype graphical shell replacement [2012 version of Vsh](https://github.com/guitarvydas/vsh).

## PEG
PEG means Parsing Expression Grammar

[Bryan Ford's Thesis](https://bford.info/pub/lang/peg/).

PEG libraries are available in many languages, for example:

- Racket [#lang peg](https://docs.racket-lang.org/peg/index.html)
- JavaScript, e.g. [peg.js](https://pegjs.org)
- Common Lisp [ESRAP](https://scymtym.github.io/esrap/)
- etc.

## Ohm-JS

My favourite PEG library is [Ohm-JS](https://github.com/harc/ohm), since it separates the grammar from the rest of the code and has a helpful [IDE](https://ohmlang.github.io/editor/).

Separating the grammar from the rest of the code is important from a DI (Design Intent / Architecture) perspective.  All other PEG libraries that I've seen conflate details with the grammar (e.g. variables, semantic code inserted into the grammar).

# Appendix Example Bash Output

This example consists of 3 (small) *bash* files.  Double-underscore `__` replaces `/` in the file names.

Plus a script to run the whole thing.  

You should be able to create the 4 files and run the example from the command line.

## hwapp123

```
#!/bin/bash
# hwapp123
# inputs: 3 ("in"): <line of characters>
# outputs: 4 ("out"): <line of characters>
BIN=.
port_in=/dev/fd/3
port_out=/dev/fd/4
${BIN}/hwapp123__hwsub23 3<${port_in} 4>${port_out} &

```

## hwapp123__hwsub23

```
#!/bin/bash
# hwapp123__hwsub23
# inputs: 3 ("A"): <line of characters>
# outputs: 4 ("B"): <line of characters>
BIN=.
A=/dev/fd/3
B=/dev/fd/4
${BIN}/hwsub23__hwhello 3<${A} 4>${B} &

```

## hwsub23__hwhello

```
#!/bin/bash
# hwsub23__hwhello
# inputs: 3 ("in"): <line of characters>
# outputs: 4 ("out"): <line of characters>
BIN=.
cat - </dev/fd/3 >/dev/fd/4

```

## run.bash

```
#!/bin/bash
pipeOut=pipe_$RANDOM
mkfifo  ${pipeOut}
pipeIn=pipe_$RANDOM
mkfifo  ${pipeIn}

./hwapp123 3<${pipeIn} 4>${pipeOut} &

echo '<dont care>' >${pipeIn} &
cat <${pipeOut}

rm ${pipeOut} ${pipeIn}
```

# Appendix - Finesse Points

None of the following points affect this exercise.  

Skip these points on first reading.

There are a number of details which appear to help in creating larger projects (i.e. not this example).

## Namespaces

Components will have several namespaces

- *i* for input ports
- *o* for output ports
- *x* for connections
- *c* for sub-components
- *n* for everything else.

The above ports for the component hwapp123/hwsub23 might, then, be named:

- hwapp123/c/hwsub23/i/A
- hwapp123/c/hwsub23/o/B.

## Send() Upwards and Downwards, Never Sideways

In creating pluggable components, one must ensure that no dependencies exist.

Rules-of-thumb:

- components cannot name each other directly
- components can only send messages upwards to their parent components or downwards to their children components (in general, sending a message upwards transmits filtered/consolidated data, sending messages downwards transmits commands (parent sends commands to children - think business hierarchy and ORG charts)).

## Structured Message Passing

Message passing will fail to scale if it is *flat* (strongly connected graph).

Structured message-passing is to message-passing as structured programming is to programming.

Form hierarchical trees, not graphs.

## Connections

Connections contain

- the sender
- the receiver.

Senders and receivers are *ports* that belong to components on the same diagram.

We usually don't care about connection names, since we can see them on the diagram(s).  

Yet, it is sometimes useful to give names to connections to allow operating on them (e.g. in human-written scripts). 

Invent names of the form "xNN".

Named connections are not required for this exercise. 

# Appendix LangJam

https://github.com/langjam/langjam

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
