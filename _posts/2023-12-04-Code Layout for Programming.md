# Code Layout for Programming

Brainstorming.

Going down the rabbit hole of possible layout styles.  Ideas not fully formed, open for discussion.

We seem to be fixated on only one style of layout - 1D. 
- Python
- Rust
- assembler
- etc.
## 1D layout 
- (row,column)
- non-overlapping cells
- top-to-bottom
- left-to-right
- sequential, stepping
- TPL
- assembler
- Python, Rust, etc.
- text editors
- needs names (or offsets/pointers/links), due to use of linear text and references to items in other portions of the text
- names cause hidden dependencies, tight coupling
- may this should be called 1.2D
	- it's kind-of 2D, but, at a very high granularity (rows, columns)
	- grid of non-overlapping cells
	- other than overstrike and Unicode combining characters, overlapping is not allowed
- writing 
	- on flat medium
		- e.g. paper
		- e.g. clay tablets
	- even more constrained and more grid-like due to invention of printing press

TPL means Textual Programming Languages.  Currently, GPLs - General purpose Programming Languages - seem mostly to be TPLs.
## 2D Layout
- (x,y)
- DPL
	- Diagrammatic Programming Languages
- VPL
	- Visual Programming Languages
- Relational Languages?
	- Prolog
	- miniKanren
- HTML?
- Declarative?
- overlapping cells / glyphs / items
	- vector-based instead of absolute coordinates / pixels
- resizable, stretchable, skewable
- diagram editors
	- draw.io
	- Excalidraw
	- yEd
- art
	- oil painting
	- charcoal, pencil
	- medium = static 
		- e.g. flat paper
		- e.g. flat canvas 
		- e.g. wood 
		- etc.
	- tools = ink, graphite+rubber, paint, dyes, etc.
- finished product does not capture the evolution of the design (time-based info)
	- closest approximation is "bubble charts"
		- brainstorming idea from song-writing (and, probably, other fields)
		- begin with a blank piece of really big paper, e.g. flip-chart page
		- write an idea in the middle of the page enclosed in a bubble (ellipse, circle)
		- riff on the idea by branching ideas from the center off in all directions, as bubbles linked back to the center, or linked to a bubble which is transitively linked back to the center
		- very Kinopio-esque
		- very HTML / markdown hyper-link-esque
		- flat, not very hierarchical
			- final product may look very busy and non-layered
			- write-only mostly (easy for creator, hard to understand for other readers)
		- in contrast, this very point-form essay is "too linear"
			- outline form is enforced and thoughts must progress top-to-bottom, left-to-right
			- hard to understand the final result in a layered manner - a little bit at a time
			- most mind-mapping tools have this failing (exceptions: Scapple, Kinopio)
- CAD
- Schematic Capture (EE)
- doesn't need names for single view
	- (x,y) position defines objects uniquely
	- needs names to connect to other drawings
- I contend that the fundamental unit of a programming language
	- should not be the "character"
	- should be a graphical "glyph"
		- e.g. rectangle
		- e.g. ellipse
		- e.g. arrow
		- e.g. group
		- e.g. text block
	- should be resizable, zoomable
	- should not be a fixed bitmap of pixels

## 3D Layout
- (x,y,t)
	- x, y are *positions*
	- t is *time*
- early games 
	- e.g. Mario
	- often called 2D as opposed to 3D
		- where 3D is taken to mean (x,y,z) - *positions* only
- Flash?
- generally not used for final layout / specification
	- more for displaying progress of game
- cartoons
	- Disney
	- cel animation

## 4D Layout
- (x,y,z,t)
	- x, y, z are *positions*
	- t is *time*
- "3D" games
- generally not used for final layout / specification
	- more for displaying progress of game
- Unity?
- ability to "walk around" an object in (x,y,z) space

## Hierarchical Layout
Design is expressed as multiple layers, arranged in a hierarchy.

UNIX® file system is hierarchical.

Drawing editors that support layers.

Programs - 1D - are typically not very hierarchical. Programmers fake out hierarchy by using multiple functions and multiple source files and placing source files within a hierarchical file system.

Tab-based programming editors are typically not hierarchical.  Tabs are presented in a single row, flat not hierarchical.

Hyper-links are an "assembler" for forming hierarchies.  It is *possible* to arrange linked units in a hierarchical fashion, but, this is not encouraged nor enforced, i.e. the GOTO problem: deja vu all over again.

## Possible Solutions
1. Use Unicode to augment ASCII in TPLs
2. Use existing drawing editors to create DPLs which are saved out as 1D text
	- draw.io (mxGraph format, inherits from XML)
	- Excalidraw
	- yEd
	- ???
	- use TPL parsing tools to parse as text, then use standard compiler techniques
		- BNF
		- e.g. CFGs, like YACC, etc.
		- e.g. PEGs, like OhmJS, etc.
			- more powerful then CFGs for describing parsers
	- Drawware, 0D - my ideas towards creating DPLs using off-the-shelf technologies
3. Flow Based Programming - FBP
	- FBP
	- DrawFBP
	- noFlo
	- Flyde
	- etc. etc.
1. remove inherent sequentialism
	- 0D
	- Relational Languages
	- UNIX® shell pipelines
	- Note that Scratch, Blockly, etc. are fundamentally sequential
		- sequentialism blocks layout innovation
# Appendix - See Also

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
