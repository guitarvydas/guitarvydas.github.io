# The Meaning of Layout
# TL;DR

I conclude that VPLs are a much better way to program than using text-only programming languages.  After all, text-only PLs are, but, 1950's caveman IDEs for programming.

I conclude that auto-layout is downright evil and counter-productive.
# Further Discussion

"Layout" conveys meaning.  It is like "syntax", but, on a higher plane.  A machine can't decide what meaningful layout is.

Dynamic layout is bad.  In fact, dynamic *anything* is bad.  

The Architect *must* decide what the layout is to be and *must* express the layout manually.  Hopefully, the Architect can do so using tools that don't stand in the Architect's way and actually help to create the layout more quickly without interjecting automation's own ideas about what the Architect means to say.  Automation should help the Architect, not guess at what the Architect intended.

If you don't understand the meaning of some visual code, don't blame the tool, blame the Architect. I consider Obsidian's "graph view" to be a disaster.  Obsidian's graph-view is based on physics, forces, etc.  It changes layout on a whim - the layout is never the same twice.  If you make a minor edit, the layout may change radically. That's the worst possible outcome.  Small edit -> big change in appearance.

- "*no easy way to add nodes in the middle of a flow without having to reorganise*" - Yep. That's the tool's fault.  The tool must make it easier for the Architect to express meaningful meaning. Automation-mania is causing editing tools to go in the wrong direction (more complication and automation, but, less control for the Architect).  I am reminded of Drakon's "smart editor". It is simple and doesn't really understand what you are drawing (a Good Thing), but, it does know enough to push boxes and skewers aside to make room for new boxes and skewers.  A simple first-step towards this kind of thing would be to allow the Architect to select a bunch of nodes and wires and to move them over en masse. I know how to do this in draw.io and I don't find myself wishing that draw.io gave me more features in this regard.  If there was a gesture that did this for me, I would probably use it, but I don't see myself making feature requests for such a thing, i.e. this kind of thing is not very important in the overall scheme of things, IMO, given the basic select-and-move-while-stretching-connections gestures that are already in the basic tool.

- "*zooming out far enough to get a good sense of the overall layout leaves you unable to read any labels*" That's a Good Thing IMO.  Psychologists say that normal humans can understand approximately 7±2 things in one gulp.  Zooming out far enough to get a good sense of the overall layout should be enough to get a good sense of the overall layout, without complicating understanding by being forced to drink from a fire-hose of details.  Zooming out should *elide* details, but, not *delete* details.  If you don't get a good sense of what's going on after zooming out, then it's the Architect's fault - the design has not been expressed cleanly, and, in a structured manner.  Gabriel Grinberg's Flyde tool has some interesting ideas about how to elide details while maintaining structured control flow.

- "*I find it easier to scan and understand the top-down flow of textual code than nodes*" -  My default is to arrange nodes and arrows and control flow in a top-down, left-to-right sequence (box, box, box, newline, box, box, box, newline, ... with arrows between the boxes and "newline" represented as an arrow that goes down and back to the front).  When I approach the Rule-of-7 limit, though, I tend to want to lasso a bunch of boxes and to abstract them into a single box, pushing the details down into a sub-level.  This is where most diagram editors fail.  It should be simple to create a wiki-link to another diagram (and a backlink from there), but, this requires too many moving parts to make it happen (if it can be done at all).  Being *able* to do something ain't the same as *making it easy* to do something.  UX is very sensitive to minor perturbations.  Most programming tools essentially go out of their way to break programmers' state of *Flow*. A current favourite tool of mine is `Kinopio`, which allows me to create sub-pages and to push large lumps of detail over to the sub-pages, yet doing so takes several gestures on my part and interrupts my train of thought.

- A paper from the past re. Experts and Novices
	- some paper I read in the past claimed that experts "see" patterns and idioms
	- "experts" can be instantly turned into "novices" by code the doesn't use, and/or mis-uses, idioms
	- "experts" can understand code faster when it is written in familiar patterns
	- "experts" are no better than "novices" when trying to understand code written with unfamiliar patterns
	- I do not have a reference to this paper

- A possible counter-argument to much of the above...
	- or, does this argument actually support much of the above?
	- *code formatting and pretty-printing*
	- some modern languages specify format as part of the language spec
		- this sounds similar to formalization of drafting rules taught by Engineering schools
	- there was lots of fumbling around with formatting in the early days ("should the open brace be at the end of the line or on the next line?")
		- this fumbling-around was, in essence, ad-hoc experimentation
			- opinion-based instead of measurement-based

- visual layout has been heavily used in the past
	- Engineering school teaches (taught) drafting, i.e. university-level courses in strict layout rules
	- EE schematics
	- mechanical CAD drawings
		- Mech Engineers are taught to make 3 static views of an object in question (front view, top view, side view)
	- previous ideas about layout are constrained by the medium - paper
		- we now have a dynamic medium that can unfold over time - computer graphics and computers
		- all the previous ideas about layout (esp. using text-only) might no longer be valid

- "... VPLs: much lower density ..." This is a Good Thing.  High-density programming languages are for brainiacs and ivory-towerists and programmers who think that details are fun.  Most people (99.9999%?) don't care about the details of programming and computers, they just want to get something done using help from automated devices.  The ultimate goal is to help normal people, not just programmers.  For example: most of us don't need to know the intricacies of Thermodynamics to use a refrigerator.  Even fridge thermodynamics physicists don't need to know everything about mechanical CAD and various aspects of Design and colour choice, and Electrical Engineering and electrical codes in various countries, etc.

- The idea of VPLs seems to be conflated with the notion of parsing full-blown Art, whereas, we don't blink an eye when text-only programming languages use only a small handful of words from the English language.  I would suggest starting very simply - parse rectangles, ellipses, arrows, blocks of text, grouping.  The big differences between VPLs and text-only programming languages include:
	- time
		- aka "sequencing"
	- vector graphics instead of bitmaps (i.e. characters)
		- e.g. with vector graphics, a programmer/architect can resize a rectangle, but it remains recognizable and parsable as a rectangle

- Eschew auto layout until we have a syntactic/semantic theory for what layout means
	- experiment, yes 
		- but, then understand why something works and/or why it doesn't work
		- develop a "theory" about what layout means, what information is carried by layout (specific to making programs "readable")

- text-only languages should have 2 syntaxes
	- one syntax to make the code easier to write
	- another syntax to make the code easier to read
	- modern parsing tools (PEG, OhmJS, etc.) make this previously-thought-to-be-a-decadent-luxury easily realizable, i.e. it is easy - now - to create new syntaxes at the drop of a hat

- text should come with a "knob" that can be turned to make the text more dense (e.g. Greek letters) for experts or less dense (long, meaningful phrases) for newbies
	- each "variable" should have several names (dense ... less dense) and each variable should have a separate "knob"

- tooltips
	- tooltips are but early-stage interface ideas that could be used for enhancing readability of code and phrases
	- problem with tooltips: not always available, i.e. hard to program into a system, essentially an after-thought
	- problem with tooltips: the gesture - hovering the mouse and waiting for some unspecified amount of time - is clunky and not precise-enough

## See Also

### References

[https://guitarvydas.github.io/2021/12/15/References.html](https://guitarvydas.github.io/2021/12/15/References.html)

### Blogs
[blog](https://guitarvydas.github.io/)

[obsidian blogs](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx-)
### Videos
[videos - programming simplicity playlist](https://www.youtube.com/@programmingsimplicity2980)
### Books
leanpub'ed (disclaimer: leanpub encourages publishing books before they are finalized - these books are WIPs)
[Programming Simplicity Takeaways, and, Programming Simplicity Broad Brush](https://leanpub.com/u/paul-tarvydas)
### Discord
[Programming Simplicity](https://discord.gg/Jjx62ypR) all welcome, I invite more discussion of these topics, esp. regarding Drawware and 0D
### Twitter
@paul_tarvydas
### Mastodon
(tbd, advice needed re. most appropriate server(s))

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
