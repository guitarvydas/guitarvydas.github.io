
# ECS Revisited
"ECS" is a paradigm that is used for programming games.  The acronym stands for Entity, Component, System.

# Comparing Implementations
These two pieces of code accomplish the same things:

Simple Lisp:
```
(let all-ents (list
    (list (cons 'tag 'player)
          (cons 'pos (make-instance ECS-Position
          (cons 'face (make-instance Facial-Expression)
    (list (cons 'tag rock)
          (cons 'pos (make-instance ECS-Position)
```

Common Lisp CLOS:
```
(defclass Entity ()
  ()
  )

(defclass Playing-Character (Entity)
  ((pos :type 'Movable :accessor pos :initarg :pos)
   (face :type 'Facial-expression :accessor face :initarg :face))
  )

(defclass Stationary-Item (Entity)
  ((pos :type 'ECS-Position :accessor pos :initarg :pos))
  )

```
Both versions compose *entities* by using *composition*, not *inheritance*.  *Composition* provides more flexibility - new fields can be added at a later time.  In the simple case, we simply stick new things into the various lists, and, in the CLOS case, we simply modify the `defclass` declarations or call the appropriate functions to do so at runtime (the data structure is not rigidly fixed at compile-time in CLOS).  In the simple case, the data structures become hoarier over time and start to become complicated.  In the CLOS case, the complexity begins immediately - programmers need to read and remember a bunch of legalese and niggly details.  In Common Lisp, you can still use a REPL at design-time.  This reduces development time.

- `defclass` is a *declarative* method for describing the data
- it is possible to add fields on-the-fly, since CLOS itself is written in Lisp and allows introspection, i.e. you can tinker with the innards of classes at runtime
	- N.B. this ability to introspect is why Common Lisp IDEs are much friendlier and easier to build
	- N.B. other languages - like Smalltalk - keep the class structure around at runtime, which, again, makes it easy to build IDEs for them
	- of course, having such power at your fingertips makes it possible to blow your own feet off and to create mysterious bugs, but, you can't have both, ease of development vs. tight checking
- most programmers don't add fields on-the-fly, they treat CLOS classes like *classes* in other languages (and, because, tinkering with running code at runtime can cause mysterious bugs, yet, tinkering is *exactly* what you want to do when developing solutions to problems), in fact, I can't remember what the tinkering functions are, I would have to look them up
	- you can see some of the tinkering (aka "introspection") functions being used in the adjunct code - e.g. the introspection function `slot-exists-p` is used in `systems.lisp` 
- `defclass` is a convenience macro that does the tinkering for you, so you don't have to remember such details for a majority of the code that you write.

CLOS is unlike most class-based systems, e.g. like "classes" in Racket or other statically-typed languages. In CLOS, "classes" can be built at runtime, whereas in most other languages, "classes" must be pre-compiled at compile-time, and, hence, give very little flexibility at design-time.

The Big Win here is the use of *composition* instead of *inheritance*.  With *composition*, you can add / remove fields on-the-fly, whereas with *inheritance* it is customary to cast data-design in stone at compile time.  CLOS is usually used with *inheritance*, but the code above doesn't work that way.  The *inheritance* used in the above code is to appease the type-checker and to declare to the reader which things are Entities and which are something else. The type-checker guarantees consistency, like declaring variables does.  If you make a typo, the variable-declaration checker alerts you. If you try to use a non-Entity as an Entity, the type-checker alerts you.

On the other hand, both pieces of code above suffer from huge disadvantages:

1. ad-hoc lack of *locality of reference* in the simple version
	- the code *knows* how the data is constructed
		- the structure of data is hard-wired into the code
	- use of raw `list` and `cons` functions make it easy to construct the data structures in a simple (non-verbose) way, but, 
	- this makes it difficult to change things later when you want to optimize and production engineer the code
		- it's like anti-DRY (Don't Repeat Yourself) for data structure design
		- the design of the data structure is sprayed and repeated in an ad-hoc manner throughout the codebase
		- when the *design* has settled down, it is usually possible to optimize the code in ways that raw uses of `list` and `cons` don't offer
	- OOP almost solved this problem, but, made the mistake of conflating data structure with control flow, so, in OOP, data is well-encapsulated, but control-flow is not well-encapsulated
2. verbosity 
	- the CLOS version suffers from extreme verbosity - anti-KISS
	- Common Lisp covers a lot of edge-cases encountered in data structure design, but, that means that programmers need to remember a big pile of niggly details


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
