Ongoing thoughts... Stream of consciousness...

Consider (> 3 2) which generalizes to (> x y)

### linear, sequential, synchronous
load R0,x
load R1,y
cmp R0,R1
brgt *label*
### human readable
x>y
### machine readable
#### CST

![](/diagrams/2023-09-19-Recursive%20Text%202023-09-19%2015.37.12.excalidraw.svg)

#### CST reduced to textual form
`(> x y)`

## Recursive Text Primitives
1. Lists
2. Atoms
3. Whitespace

Lists can contain all 3 types of primitives.  Lists are, hence, recursive.

Atoms are the *bottom*.  Atoms are not recursive.

Whitespace is noise / discardable, but, acts as separations between Atoms, between lists.

Separator = "(" | ")" | space
Atom = anything but Separator
List = "(" [List | Atom | Separator]* ")"

## Syntax
1. Human readable
2. Machine readable

It is a mistake to conflate the two.

see 2023-09-19-Syntax
## Expressiveness
In my opinion, it is not sufficient to simply "model" time using a time-less notation.  

see 2023-09-19-Expressiveness

## The Problem With General Purpose Programming Languages
The idea of GPLs (General Purpose programming Languages) was developed when it was believed that the act of building languages was time consuming and difficult and a black art.

This assumption is no longer true (due to the advent of PEG technologies, and decades of research).

Yet, we continue down the path of inventing new kinds of GPLs at the exclusion of inventing ways to bolt disparate languages together to build solutions to problems.

GPLs are but wishy-washy unions of features needed to solve certain problems perceived by the inventor(s) of specific GPLs.  New GPLs are invented frequently (daily, weekly?), yet, all GPLs are based on the same-old, same-old features:
1. GPLs are all sequential (like assembler)
2. GPLs are based on the ideas of functions
3. GPLs assume that everything can - and should - be synchronized.

## CPUs are Not Computers
CPUs are electronic chips invented by electronics hardware manufacturers.  CPUs contain instructions named CALL and RETURN.  These instructions were *not* invented to support functions.  

see 2023-09-19-CPUs Are Not Computers


## See Also
### Blogs
https://publish.obsidian.md/programmingsimplicity (see blogs that begin with a date 202x-xx-xx-)

https://guitarvydas.github.io/
### Videos
https://www.youtube.com/@programmingsimplicity2980
### Books
leanpub'ed (disclaimer: leanpub encourages publishing books before they are finalized)
https://leanpub.com/u/paul-tarvydas
### Discord
https://discord.gg/Jjx62ypR  ("programming simplicity") all welcome, I invite more discussion of these topics
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
