---
layout: post
title:  "Racket Switch Macro"
---

# Introduction

Deconstruction of `switch` macro in Racket.

[switch macro discussion on Stack Overflow](https://stackoverflow.com/questions/32793972/racket-switch-statement-macro)

# Prerequisites

The Racket compiler allows programmers to define macros which get inserted into the compilation phase.

<img src="/Users/tarvydas/Library/Application Support/typora-user-images/image-20210912174055684.png" alt="image-20210912174055684" style="zoom:67%;" />

Racket macros are written in Racket and operate on `syntax` objects.

[_aside: The Racket compiler manipulates `syntax` objects.  The Lisp (a precursor to Racket) compiler manipulates `lists`._]

`STX` usually denotes a `syntax object`.


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
The `require` is used to set up the compiler for macro processing [_don't worry about what this means for now_.]

The macro is called `switch` and is defined in the `define-syntax` form.

The macro uses 2 auxiliary functions, `transform-clause` and `transform-clauses`.  

The main body of the macro is in the `(syntax-case stx () ___)` clause.   [_For now, don't worry about the meaning of () as the second part of the syntax-case_].

`Test2` is the test of the macro.  `Test1` is the equivalent code using the builtin `case` form.

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
