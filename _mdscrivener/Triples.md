Title: Triples  
Author:

# Triples #

Triples are everywhere, albeit optimized into oblivion.

The major simplicity that I have known for years — and unable to express succinctly — is that compiler-people like triples.

I, also, call this "divide and conquer".  [If you think of a better way to say that, let me know!].

# XML #

AFAIK, xml started out life as triples.  (This doesn't mean that I am right, it is only what I believe) 

Example of RDF triples: 
https://www.iro.umontreal.ca/~lapalme/ForestInsteadOfTheTrees/HTML/ch07s01.html



## Example ##


An example is given here 

https://www.javatpoint.com/xml-example


<?xml version="1.0" encoding="ISO-8859-1"?>  
<note>  
  <to>Tove</to>  
  <from>Jani</from>  
  <heading>Reminder</heading>  
  <body>Don't forget me this weekend!</body>  
</note>


## As Triples ##

note id234 null
from id234 "Jani"
to id234 "Tove"
heading id234 "Reminder"
body id234 "Don't forget me this weekend!"

# Computer Science #

All of CS breaks down into triples — something I call "simple".

All of CS has been about trying to optimize triples to save space and CPU.  

Very 1950's.  

In 202x's, memory is cheap, CPU's are cheap.  

Time to rethink.

Human-time is still expensive.  

Waste computer-time, not human-time.

# Data Structures #

Data structures are just optimizations of triples

Data structures at compile-time are

* 1950's notions of how to optimize for CPU usage
* Design Intent (more human-readable, but hard to automatically optimize)

# Curried Functions #

Even curried functions are triples

 fn x y -> (fn x) y

(fn x) y -- looks like a double, but is really a triple — relation=fn, subject=x, object=y.  

"(fn x)" is a double.  

"(fn x) y" is a triple.  

"(fn x)" is an unresolved triple.


# PROLOG #

PROLOG allows you to go into feature-itis, creating quadruples, quituples, etc., but they are just optimizations of things that are fundamentally triples.

Anything in PROLOG that is "more than" a triple is a layer.

PROLOG is (can be):

* describe problem as relations (triples)
* waste CPU power rebuilding data structures (better than wasting human intellectual power).

# Human Readability #

Humans shouldn't have to read triples.  

But, if you deconstruct everything into triples, then it becomes easier to write DSLs and the like.
