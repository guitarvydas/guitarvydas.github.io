---
layout: post
title:  "Parsing Diagrams - Bounding Boxes"
---
Parsing a simple diagram and creating bounding boxes for all rectangles on the diagram.

# Diagram

Screenshot of app.diagrams.net (drawio) showing a simple diagram.

Highlighted:

- the box H

- it's (x,y), width and height

  
  
  ![2021-07-25-diagram.png](https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-07-25-diagram.png?raw=true)

# Facts

The diagram converted to a textual factbase for PROLOG. [_In this example, I will use PROLOG (SWIPL), but the work can be done in just about any language, e.g. Python, miniKanren, clojure (see also, core.logic), Datalog, JavaScript, etc.  PROLOG provides automated backtracking which can be replaced by loops/recursion in other languages._]

![2021-07-25-facts.png](https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-07-25-facts.png?raw=true)


The diagram facts are stored in the file `diagram.pl`.

# Rect and Name Facts

Add `rect` and `name` facts.

Triples are

- relation
- subject
- object.

We use triples strictly. 
Facts that are doubles, like `rect`, are written as triples with an empty 3rd item.

We emphasize *machine-readability*.  Normalization and repetition is better for machines, but looks like noise to humans.  For example, human readers can infer the names and don't need empty 3rd items, but, such redundancy makes it easier for machines to parse.

![2021-07-25-rect and name facts.png](https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-07-25-rect%20and%20name%20facts.png?raw=true)

# Bounding Boxes

A bounding box is a simple rectangle that encompasses a graphical object.

A bounding box consists of four numbers:

- left
- top
- right
- bottom.

Diagrams.net gives us x, y, width and height.

To make a bounding box from the information we simply calculate:

- left is X
- top is Y
- right is X+Width
- bottom is Y+Height.

[_(0,0) is at the top-left_]

We can write code to calculate the bounding box.  

Below is the SWIPL PROLOG code.  Explanation of the code follows.

```
makebb(ID):-
    rect(ID,_),
    x(ID,X),
    y(ID,Y),
    w(ID,Width),
    h(ID,Height),
    format("l(~w, ~w).~n", [ID,X]),
    format("t(~w, ~w).~n", [ID,Y]),
    W is X + Width,
    format("r(~w, ~w).~n", [ID,W]),
    H is Y + Height,
    format("b(~w, ~w).~n", [ID,H]).
  

```

The PROLOG code says:

- All `,`-separated clauses are *and*'ed together

- ID must be a rect

- ID must have x, y, w and h facts

- Assign the values of x, y, w and h into PROLOG variables X, Y, Width and Height

- Print 4 lines of output using the *format* directive

  - left is just X

  - top is just Y

  - right is X + Width

  - bottom is Y + Height.

    

    We see the result for object *h*.

![2021-07-25-bounding box for h.png](https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-07-25-bounding%20box%20for%20h.png?raw=true)


## Details

The details of running this simple query are shown below, if you want to follow along.

![2021-07-25-details bounding box for h.png](https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-07-25-details%20bounding%20box%20for%20h.png?raw=true)

[_N.B. The details should be boring to human readers. Repetition and simplicity are keys to machine readability and writing code that writes code.  The code for the above has been put into a bash script called bb.bash to emphasize the fact that this process can be automated._ ]

# Bounding Boxes For All Objects

We add the following code to the swipl query to loop over every `rect` printing the bounding box for each. Again, note that this could be done in any language.

```

makeAllBB:-
    bagof(ID,makebb(ID),_).

```

Details: `bagof` runs makebb(ID) for every ID.  It collects the results in a bag (warning: comp sci term).  We discard the results using the `_` character.  We don't care about the actual results, only the print-out[^1].

[^1]: This code produces a side effect. We could get rid of the side effect and make this more FP'ish, but why bother?  We don't need FP to express 14 lines of code. [_N.B. We will endeavour to keep things simple, by minimizing the code line count._]

# Simplicity

Simplicity is defined as *lack of nuance.*

# Lack of Detail (at this layer)

It might appear that this treatment does not include enough details for converting diagrams to code.

This is a hallmark of the *layered* approach - each layer can be understood in its entirety without confronting all of the details.

As we will see in subsequent essays, we *will* add enough details - in layers - to compile this diagram to code.

The only difference between this *layered* approach and other approaches is *where* the details appear.

There is no need to *flatten* the information contained in this diagram.  Details will be supplied in lower layers, but will not affect the appearance of this layer.  

The goal is to make *every* layer as simplistic as this one.

# Factbase Growth

There is no current need to prune the factbase.

Pruning is an optimization, only.

Unneeded facts are skipped by the factbase engine.  The rules use only the facts that are needed.

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
