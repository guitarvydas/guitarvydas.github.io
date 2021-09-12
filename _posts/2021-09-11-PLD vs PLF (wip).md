---
layout: post
title:  "PLD vs PLD (notes)"
---

In this essay, I use the abbreviations:
- PLD to mean Programming Language Design, and,
- PLF to mean Programming Language Fundamentals.

Both, PLF and PLD are necessary for creating a popular programming language.

if-then-else
counting parameters
# parameter counting - lisp vs pascal 
---
/* C */
void fn (int x, int y) {
}

void tester () {
  fn (1, 2);
  fn (1);
}
---
// JavaScript
function fn (x, y) {
}

fn (1, 2);
fn (1);

---
# syntax for `end if`
-- (fn x) fn(x), (if x y) if x then y end if
# assembler
-- no syntax
syntax, the realm of syntax
JS vs C
fn(x,y) fn(x,y), JS doesn't count args
variable args
AGDA syntax vs. Smalltalk syntax
Architecture vs Engineering (vs construction)
type checking
-- another layer of checking, like application of syntax
interpretation vs compilation
-- all languages must be interpreted
-- compilation is an optimization the pre-interprets some of the code
-- the optimization called "compilation" might require some changes to the language to allow the optimization
# error messages and warnings
--------
(defun fn (x y)
  (declare (ignore x y)))

(fn 1 2)

(fn 1)
--------
While evaluating the form starting at line 6, column 0
  of #P"/Users/tarvydas/Desktop/junk.lisp":

debugger invoked on a SB-INT:SIMPLE-PROGRAM-ERROR in thread
#<THREAD "main thread" RUNNING {1001570143}>:
  invalid number of arguments: 1

Type HELP for debugger help, or (SB-EXT:EXIT) to exit from SBCL.

restarts (invokable by number or by possibly-abbreviated name):
  0: [REPLACE-FUNCTION] Call a different function with the same arguments
  1: [CALL-FORM       ] Call a different form
  2: [RETRY           ] Retry EVAL of current toplevel form.
  3: [CONTINUE        ] Ignore error and continue loading file "/Users/tarvydas/Desktop/junk.lisp".
  4: [ABORT           ] Abort loading file "/Users/tarvydas/Desktop/junk.lisp".
  5:                    Exit debugger, returning to top level.

(FN 1) [external]
   source: (DEFUN FN (X Y) (DECLARE (IGNORE X Y)))
0] 
--------

# PLF vs PLD
PLF vs PLD
.. plf is rigor
.. pld is ux
... is there Science for UX?
.. at, ae ai aa arch, eng implement
.. how is an arch diff from an eng?
.. how is an eng diff from an implementors?
.. read and write syntax
.. Das is deeper syntax than only text
... SVG
.. languages need not be restricted to non overlapping cells of small bitmaps

.... keyboard keys are bound to bitmaps

.. backtracking to parser chars, but to parser diagrams
.. design is about fewer details,  smartness is about juggling large soup of details 
.. classes are compile time, prototypes are runtime

# locality of reference

# C vs Assembler

# Pascal vs C

# Smalltalk vs Assembler

# Assembler vs Identifiers

Why Spaces Are Not Allowed in Identifiers

|abc def|



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
