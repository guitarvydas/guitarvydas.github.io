---
layout: post
title:  "Racket Peg Case Forms"
---

# Introduction

We show one way to use PEG in Racket, to emit a _case_ form.

# Sample

We transpile

```
1 'a $ 2 'b $ 3 'c $ 4 'd $ else 'e
```

and expect to get Racket case code:

```
(lambda (k) 
  (case k 
    ((1) 'a) 
    ((2) 'b) 
    ((3) 'c) 
    ((4) 'd) 
    (else 'e)))
```

This constituted an experiment, so we explicitly wrote the case labels and we used `$` to separate the cases.  

Other variations of the syntax should be possible.

# PEG Code
The essential grammar is:
```
#lang peg
pclause <- s-exp _ s-exp;
pelseclause <- 'else' _ (s-exp);
pclauses <- (pelseclause / pclause) (_ '$' _ pclauses)?;
pcasetest <- pclauses;
```
The essential action code is appended to the grammar:
```
#lang peg
pclause <- caselabel:s-exp _ e:s-exp -> (list (list caselabel) e);
pelseclause <- 'else' _ (e:s-exp) -> (list 'else e);
pclauses <- cl1:(pelseclause / pclause) (_ '$' _ cl2:pclauses)? -> (if cl2 (cons cl1 cl2) (list cl1));
pcasetest <- cls:pclauses -> (list 'lambda '(k) (cons 'case (cons 'k cls)));
```

To make this work, we need to add some Racket code.  `#lang peg` requires that such code appear before any PEG code.

The full code is:

```
#lang peg
(require "../racket-peg/s-exp.rkt");
(define (compile-snippet e) (eval e));
(define (ptest k)
  (let ((pexpr (peg pcasetest "1 'a $ 2 'b $ 3 'c $ 4 'd $ else 'e")))
    (let ((e (compile-snippet pexpr)))
      (println (e k)))));
pclause <- caselabel:s-exp _ e:s-exp -> (list (list caselabel) e);
pelseclause <- 'else' _ (e:s-exp) -> (list 'else e);
pclauses <- cl1:(pelseclause / pclause) (_ '$' _ cl2:pclauses)? -> (if cl2 (cons cl1 cl2) (list cl1));
pcasetest <- cls:pclauses -> (list 'lambda '(k) (cons 'case (cons 'k cls)));
```

Note that order matters in PEG. `Pelseclause` must be tried before `pclause` in the rule `pclauses`.

Note that I prefixed every rule with the letter `p` to keep it distinct from the raw Racket code (below). Such prefixing is not necessary - I used prefixing only during bootstrapping wherein I wanted to keep the raw Racket code alongside of the PEG code.

To test this, simply run (ptest 3) and (ptest 99).

# Raw Scheme Code
Without `#lang peg`, but using the peg library, the raw Racket code is:
```
#lang racket

(require peg)
(require "../racket-peg/s-exp.rkt")

(define-peg clause
  (and (name caselabel s-exp) _ (name e s-exp))
  (list (list caselabel) e))

(define-peg elseclause
  (and "else" _ (name e s-exp))
  (list 'else e))

(define-peg clauses
  (and (name cl1 (or elseclause clause))
      (? _ #\$ _ (name cl2 clauses)))
    (if cl2
      (cons cl1 cl2)
      (list cl1)))

(define-peg casetest
  (name cls clauses)
  (list 'lambda '(k) (cons 'case (cons 'k cls))))

(define (compile-snippet e) (eval e))

(define (test k)
  (let ((pexpr (peg casetest "1 'a $ 2 'b $ 3 'c $ 4 'd $ else 'e")))
    ;(println pexpr)
    (let ((e (compile-snippet pexpr)))
      (println (e k)))))
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
