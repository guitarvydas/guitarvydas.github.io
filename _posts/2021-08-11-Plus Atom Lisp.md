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

## Assembler Directives

The assembler program converts human-readable mnemonics into binary form.

The assembler is line-oriented, i.e. one statement per line.

The assembler assumes that all addresses/offset are byte-oriented.  

Addresses/offsets are integers in the range 0-65535.

Labels begin in column 1, all other statements begin after column 1.

The assembler makes 2 passes over the code:

1. Determine the location of all labels
2. Convert mnemonics into binary.

### *

`*` *here* - denotes the current binary offset of the *beginning* of the line.

'*' in column 1 creates a comment (to end of line).

The assembler uses a small set of *directives* that emit no binary.

### EQU

The `EQU` directive equates a label to a value.  

Usually, the value is `*`, in which case the directive sets the value of the label to the current location of the line in the binary.

Example: `OBL28 EQU *` means to set the label `OBL28` to be the offset of the current line.

Example: `*+4` means  *the offset of here plus 4*

### FDB

`FDB` initializes "double" words, i.e. 2 bytes.

FDB uses comma-separated arguments and created 2 bytes for each given argument.

Example: `FDB *+4,OBL29` means to initialize 4 continguous bytes.  2 bytes hold *here* plus 4, the next two bytes are initialized to the integer offset of `OBL29`.

### FCC

`FCC` initializes single bytes.  

Strings of byte-sized characters (ASCII) are surrounded by single quotes.

Example: `FCC 'PL' `means to initialize 2 bytes, the first to the ASCII value of P (0x50 hex, or 80 decimal) and the second byte is initialized to the ASCII value of L (0x4C hex, or 76 decimal).

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
