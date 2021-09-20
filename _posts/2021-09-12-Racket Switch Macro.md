---


layout: post
title:  "Racket Switch Macro"
---

# Introduction

Deconstruction of `switch` macro in Racket.

[switch macro discussion on Stack Overflow](https://stackoverflow.com/questions/32793972/racket-switch-statement-macro)

# Prerequisites

The Racket compiler allows programmers to define macros which get inserted into the compilation phase.

<img src="https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-09-12-Racket%20Compiler.png?raw=true" alt="2021-09-12-Racket Compiler.png" style="zoom:67%;" />

Racket macros are written in Racket and operate on `syntax` objects.

[_aside: The Racket compiler manipulates `syntax` objects.  The Lisp (a precursor to Racket) compiler manipulates `lists`._]

`STX` usually denotes a `syntax object`.

I use `___` for elision, avoiding `...`, since that is used as syntax in Racket macros.

`#'` creates a syntax object from a Racket expression.

Macros are *functions* that execute at compile-time.  Macros manipulate the original source code and expand into final source-code.


# Top Layer
```
#lang racket
;; see https://stackoverflow.com/questions/32793972/racket-switch-statement-macro

(require (for-syntax syntax/parse))

(define-syntax (switch stx)
  (define (transform-clause cl)
     ___

  (define (transform-clauses cls)
     ___

  (syntax-case stx ()
     ___

(define x 5)

(define (test1)
  ;; uses builtin 'case'
  (case x
    ((3) (displayln "x is 3"))
    ((4) (displayln "x is 4"))
    ((5) (displayln "x is 5"))
    (else (displayln "none of the above"))))

(define (test2)
  ;; uses macro 'switch'
  (switch x
          [3 (displayln "sw x is 3")]
          [4 (displayln "sw x is 4")]
          [5 (displayln "sw x is 5")]
          [default (displayln "sw none of the above")]))

(test1)
(test2)
```
The `require` is used to set up the compiler for macro processing [_don't worry about what this means for now_.]

The macro is called `switch` and is defined in the `define-syntax` form.

The macro uses 2 auxiliary functions, `transform-clause` and `transform-clauses`.  

The main body of the macro is in the `(syntax-case stx () ___)` clause.   [_For now, don't worry about the meaning of () as the second part of the syntax-case_].

`Test2` is the test of the macro.  `Test1` is the equivalent code using the builtin `case` form.

# Layer 1

```
(syntax-case stx ()
    ((_ x clause ...)
     (with-syntax (((case-clause ...) (transform-clauses #'(clause ...))))
       #'(case x case-clause ...)))))
```

The `_` is a short-hand for the macro name, in this case `switch`.

Looking at `test2`, the compiler (macro expander) sees a `switch` expression:

```
  (switch ___)
```

and binds the three variables:

```
  x <= x
  clause <= 
          [3 (displayln "sw x is 3")]
          [4 (displayln "sw x is 4")]
          [5 (displayln "sw x is 5")]
          [default (displayln "sw none of the above")]
  ... <=
```



This says that when the compiler matches an expression starting with `switch`, it will bind the second item (of the expression) to `x`, the third item to `clause` and lump all of the rest of the items into `...`.

`x` and `clause` and `...` can only be used in syntax manipulation expressions.

`clause` is used in the `#'(clause ...)` expression which forms the argument to the auxilliary function `transform-clauses`.

`with-syntax` does more (recursive) pattern-matching.  The result of `transform-clauses`is matched and bound to `case-clause`.

The final `#'(case x case-clause)` expression uses the two bound syntax variables, `x` and `case-clause` and returns a syntax expression that forms a `case` expression.

That returned expresssion is fed to the macro-expander part of the compiler which feeds into the rest of the downstream compilation.  Hence, whereever `(switch ___ ___ )` appears in the code, it will be replaced by the expanded macro (a `case` expression, in this instance).

# Layer 2

```
  (define (transform-clauses cls)
    (syntax-case cls ()
      ((cl)
       (with-syntax ((case-clause (transform-clause #'cl)))
         #'(case-clause)))
      ((cl rest ...)
       (with-syntax ((case-clause (transform-clause #'cl))
                     ((case-rest ...) (transform-clauses #'(rest ...))))
         #'(case-clause case-rest ...)))))
```

The auxiliary function `transform-clauses` takes one parameter, named `cls`, and performs a syntax-based pattern-match.  

`Cls` is of type `syntax`.

The first clause `(cls)`matches the degenerate case of a single clause.  It calls `transform-clause` and returns that syntactic value.  To perform the return, it pattern-matches the result of `transform-clause`, binds the match to `case-clause`, then returns `case-clause` as a `#'` syntax object.

The other clause `(cl rest ...)` matches the case of multiple clauses, binding the matches into variables `cl`, `rest` and `...`.

```
cl <=
          [3 (displayln "sw x is 3")]
rest <=
          [4 (displayln "sw x is 4")]
          [5 (displayln "sw x is 5")]
          [default (displayln "sw none of the above")]))
```

The macro expansion is performed recursively until the degenerate case (`[default ___]`) is reached.

```
cl <=
          [4 (displayln "sw x is 4")]
rest <=
          [5 (displayln "sw x is 5")]
          [default (displayln "sw none of the above")]))
```

```
cl <=
          [5 (displayln "sw x is 5")]
rest <=
          [default (displayln "sw none of the above")]))
```

```
cl <=
          [default (displayln "sw none of the above")]))
rest <=

```

# Layer 3

```
  (define (transform-clause cl)
    (syntax-case cl (default)
      ((default expr) #'(else expr))
      ((val ... expr) #'((val ...) expr))))
```

The auxiliary function `transform-clause` converts one clause into its final form, e.g.

```
         [3 (displayln "sw x is 3")]
```

gets bound to variables

``` 
val <= 3 
... <=
expr <= (displayln "sw x is 3")

```

and is expanded into

```
         #'((3) (displayln "sw x is 3"))
```

while the `default` clause is bound to variable:

```
expr <= (displayln "sw none of the above")
```

and expands into

```
#'(else (displayln "sw none of the above"))
```

# Complete Version

```
#lang racket
;; see https://stackoverflow.com/questions/32793972/racket-switch-statement-macro

(require (for-syntax syntax/parse))

(define-syntax (switch stx)
  (define (transform-clause cl)
    (syntax-case cl (default)
      ((default expr) #'(else expr))
      ((val ... expr) #'((val ...) expr))))

  (define (transform-clauses cls)
    (syntax-case cls ()
      ((cl)
       (with-syntax ((case-clause (transform-clause #'cl)))
         #'(case-clause)))
      ((cl rest ...)
       (with-syntax ((case-clause (transform-clause #'cl))
                     ((case-rest ...) (transform-clauses #'(rest ...))))
         #'(case-clause case-rest ...)))))

  (syntax-case stx ()
    ((_ x clause ...)
     (with-syntax (((case-clause ...) (transform-clauses #'(clause ...))))
       #'(case x case-clause ...)))))

(define x 5)

(define (test1)
  ;; uses builtin 'case'
  (case x
    ((3) (displayln "x is 3"))
    ((4) (displayln "x is 4"))
    ((5) (displayln "x is 5"))
    (else (displayln "none of the above"))))

(define (test2)
  ;; uses macro 'switch'
  (switch x
          [3 (displayln "sw x is 3")]
          [4 (displayln "sw x is 4")]
          [5 (displayln "sw x is 5")]
          [default (displayln "sw none of the above")]))

(test1)
(test2)
```
# See Also

[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC2bdO9l84VWGlRdeNy5)
[References](https://guitarvydas.github.io/2021/01/14/References.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
