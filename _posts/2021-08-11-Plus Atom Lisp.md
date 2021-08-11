---
layout: post
title:  "PLUS Atom Lisp"
---
# Introduction

We examine the ATOM structure in Frits van der Wateren Lisp 1.5.  Motorola 8-bit CPU, MC6800.

The code snippet is listed below.

# Cell Diagram for PLUS Atom

<img src="https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-08-11-PLUS-Cell%20Diagram.png?raw=true" alt="2021-08-11-PLUS-Memory Layout.png" style="zoom:67%;" />

`FDB` means initialize double bytes (addresses).

`FCC` means initialize single bytes.

# Memory Layout for PLUS Atom

<img src="https://github.com/guitarvydas/guitarvydas.github.io/blob/master/assets/2021-08-11-PLUS-Memory%20Layout.png?raw=true" alt="2021-08-11-PLUS-Memory Layout.png" style="zoom:67%;" />

# Comments

# Strings Are Tokenized

At the low-levels, this Lisp does not deal with strings.

This Lisp deals only with 4-byte cells, which have been chosen to fit the 8-bit CPU.

In this 8-bit CPU, an address is 16 bits, which is 2 bytes.

`CAR` is 16 bits (2 bytes).

`CDR` is 16 bits (2 bytes).

A `CONS` cell is 32 bits (4 bytes) - one `CAR` and one `CDR`.

## Magic Marker

Addresses are all mod(4).

Hence, the bottom 2 bits are "free".

The Magic Marker, called "M", is set to 000000001 in the address to signify a print-name.

# Code

[Frits van der Wateren Lisp 1.5](https://github.com/guitarvydas/frits-van-der-wateren-lisp/blob/master/LISP.TXT)

## Code Snippet For PLUS ATOM

```
OBL28   EQU   *
   FDB   *+4,OBL29
   FDB   *+12+M,*+4
   FDB   SUBR,*+4
   FDB   PLUS,NIL
   FCC   'PL'
   FDB   *+2
   FCC   'US'
   FDB   NIL
OBL29   EQU   *
```
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
