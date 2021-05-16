---
layout: post
title:  "Software Components 101 Part 6 Recap"
---
Thus far, we have 13 distinct kinds of facts:
1. arrow
2. arrowBegin
3. arrowEnd
4. circle
5. color
6. comp
7. cyl
8. rect
9. str
10. strokeWidth
11. text
12. aBegin
13. aEnd

Let's recap what these facts all mean.

Each fact refers to a unique ID (the Subject) and most facts contain a second ID (the Object).

Facts do one of 2 things
1. declare a unique ID for some item
2. specify a property for an item.

Facts of the form (1) have a `relation` and a `subject`.  The 3rd field - the `object` is ignored (and is usually written as `nil`).

Facts of the form (2) have a `relation` (aka property) and, both, a `subject` and and an `object`.  In this case, the `subject` refers to the ID of some item.  The `object` is an atomic property, or, the ID of a related item.

[We will be querying facts using PROLOG, so we need to wrap the `subject` and `object` in parentheses and put a period at the end of each fact.  PROLOG does not allow there to be a space between the relation name and the first open parenthesis.  The syntax will vary depending on the target query language.]

Working our way down the list:

- `arrows` declare the ID for a (unique) arrow and relate the arrow to another item (a graphical shape - rect, (comp), circle, cylinder).  `Arrow` facts are of the form `arrow(shapeID,arrowID).`  Arrow items are always accompanied by `aBegin` and `aEnd` facts which specify the arrowID and the source/target items' ID.

- `ArrowBegin` and `arrowEnd` facts are used for inferencing `aBegin` and `aEnd` facts.  After inferencing, we ignore all `arrowBegin` and `arrowEnd` facts.  These facts contain short-hand references to objects.  We get rid of the short-hand (through inferencing) early and ignore these facts.  [Instead of ignoring the obsolete facts, should we delete them?  No.  See below for a discussion].

- `Circle`, `cyl` and `rect` facts declare unique IDs for circle, cylinder and rectangle graphical items.

- `Comp` facts are like `rect` facts, but are used as short-hand for human-input.  In a fully automated system - not a bootstrap one like this one - there would be no need for `comp` facts.  Rectangles would be differentiated based on their size and containment properties.  Here, `comp` facts demonstrate the divide between human-readability and machine-readability.  Machines can easily perform the repetitive work required in sorting rectangles into two categories (components and ports), but humans cannot enter low-level information reliably and prefer to eye-ball and sort the rectangles during data entry.  Errors during data entry can be more easily spotted by humans when the rectangles are pre-sorted.

- `Text` facts declare IDs for text items and associate them with graphical items.  The format is `text(graphicalID, textID).`.  `Text` facts are alway accompanied by `str` facts which associate strings with textIDs.[^1]

[^1]: Why do we have separate `text` and `str` facts?  The reason is mostly historical - efficiency concerns with other querying languages.  Folding `str` facts into `text` facts is but an optimization.  This kind of optimization is better left to Efficiency experts using profiling tools.  We are _only_ concerned with making this design workable - low-level efficiency can be addressed later.  Our inferencing queries make this distinction invisible (be expending computing power).  Usually, efficiency concerns tend to muddy clean designs.  In this particular case, we will stick to the dogmatic expression of repetitive facts and leave efficiency concerns for later.  The only efficiency that matters, at this stage, is time-to-architect and time-to-engineer.  If our choice(s) create slow turn-around times for Architecture and Engineering, then we will optimize our choice(s) sooner rather than later.[^gradual]

[^gradual]: Optimization (and typing) should be done in a gradual manner, in layers, and, should be done on a per-project basis.  Some optimizations affect the final throughput in ways that affect the ultimate users of the solution.  This effect depends on the particular problem-at-hand and cannot be generalized.  Typing is the same - it should be done in a gradual manner, in layers.  Typing was originally invented to aid compiler-writers but has grown into a brainstorming and design technique.  What is missing is the concept of project-specific design rules.  Design rules are like typing, but based on the problem-at-hand.  An obvious example is the divide between decimal notation and binary notation for financial apps vs. digital control apps.  Several languages offer a "union" of such capabilities, while making the languages more complicated and harder to implement.  In some problem domains, we use the term "business rules" to mean problem-specific design rules.  A union of _all_ possible design rules results in spaghetti.  As we've learned time and again - scoping and nesting and restricting solutions is the best way to tame tangled design rules.  (For example, "global variables" were considered to be a problem - the solution was scoping.  GOTOs were considered to be a problem - Structured Programming (nested control flow) was the solution.).  A union cannot be achieved unless _all_ possible design rules are known before-hand.  Unions of design rules is just Waterfall thinking.  The answer is to design isolated components and to plug them together into larger and larger applications.

`Color` facts specify properties of graphical objects.  The general format of these facts is `color(shapeID,colorName).`.  Colors are specified by name - green, yellow and red are valid color names.  Shapes have no color specified by default.  We use a positive-inferencing methodology - colors are specified where they matter.  In the case of this simple example, input ports have color green.  Output ports and all other shapes do not match color=green.  Other colors are "don't cares".  Anything-but-green is ignored.

`Stroke-width` facts supply a stroke-width property for shapes.  We only care about stroke-width=3.  All other stroke-widths (including no stroke-width) are ignored and don't match stroke-width=3.  In this particular case, ports with stroke-width=3 signify implicitly connected ports.  All other ports must be explicitly connected (using arrows).  We infer explicit-vs-implicit ports early and ignore stroke-width facts after explicit/implicit facts have been created.

[N.B. Facts are built up in layers. As we add semantically-interesting facts, we can ignore the low-level, grapihical facts that were used in previous layers.  The goal is to build isolated layers of software components, instead of trying to do "everything" at once.  This maximizes the possibility for completely different interpretations of the same factbase.  For this same reason, we do not delete facts from the factbase, if possible.  Committing to a certain factbase format and/or to data structures snips off other design possibilities.[^snip]]

[^snip]: My favourite example is the idea of building a factbase that implements a full techincal project.  Imagine that your business manager walks in and asks for a Gannt Chart of the project.  This can be created in 10's of minutes if the factbase retains all data in machine-readable form.  If, though, the project is implemented in data structure format (e.g. a tree), then a walk of the structured data is required and makes the task, of producing a Gannt Chart, more difficult.  We (the royal we) are developing new technologies to perform such walks of structured information (e.g. PEG on structured text), but the human resources needed to create these technologies can be put to better - higher-level - use.  This happened in the transition from assembly code to structured programming languages.  When human resources were freed from having to deal with assembly programming, programmer creativity blossomed and we (the royal we) could attack problems in new ways (e.g. relational thinking).  What are the trade-offs and what is the best mix of such ideas and technologies?  I don't know.  But, I believe that we should leverage machines to do the repetitive work, freeing our own selves to do more creative work.  Everything is a fractal - once we scale the next layer, we can divvy up the work and give as much of it to machinery as possible, allowing us to scale the next layers.  And so on.  The divvying process should never stop.  We see this same kind of thing happening now - Python was invented to solve one kind of problem, but Python is now being used to solve A.I. problems.  We insulate ourselves from future changes by inferring information and inserting higher-level facts into the factbase - we isolate inferences based on graphical properties to their own, isolated, layer.  Each layer "produces" semantic facts that the next layer uses.  A change to the project requirements affects the inferencing at particular layers only.

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
