From Tunney's [Sector Lisp webpage](https://justine.lol/sectorlisp2/)
```
function Eval(e, a) {
  var A = cx;
  if (!e) return e;
  if (e > 0) return Assoc(e, a);
  if (Car(e) == kQuote) return Car(Cdr(e));
  if (Car(e) == kCond) return Evcon(Cdr(e), a);
  return Gc(A, Apply(Car(e), Evlis(Cdr(e), a), a));
}

function Apply(f, x, a) {
  if (f < 0)      return Eval(Car(Cdr(Cdr(f))), Pairlis(Car(Cdr(f)), x, a));
  if (f == kEq)   return Car(x) == Car(Cdr(x));
  if (f == kCons) return Cons(Car(x), Car(Cdr(x)));
  if (f == kAtom) return Car(x) >= 0;
  if (f == kCar)  return Car(Car(x));
  if (f == kCdr)  return Cdr(Car(x));
  return Apply(Assoc(f, a), x, a);
}
```

`Eval` interprets code.  The textual form of the code is, first, converted to list form, then the list is interpreted by `Eval`.

`Eval` does some preprocessing - peeling off some low-hanging fruit, then calls `Apply` to finish the work.  `Apply` executes a function (a `lambda` expression) and supplies arguments to the function (if any).

Since everything has been converted to an internal form, i.e. lists, `apply` expects to see a list in which the first argument is a *function* and the rest of the arguments (if any) are arguments to the function.  By the time `Apply` is called, all of the arguments have been evaluated.

For example, if one of the arguments is a variable - say `x` - that variable is first evaluated to be a value - a list or an atom.  If the argument is not boiled down to a low-level value, then `Eval` is called on the argument.

In the above code, `Apply` takes 3 arguments:
1. `f` the function to be used
2. `x` the argument to the function
3. `a` a map of *names* to *values* - aka "environment"
	- in this basic Lisp, the map is created using a *alist* which is just a linear list of pairs {name X value} - this has the drawback of being less efficient than a hash table, but, works well enough to show what's going on, and, works well enough when the environment isn't very deep

`Eval` always returns a value.  In Lisp, *everything* returns a value - Lisp is an expression-based language, instead of a statement-based language.  Everything is an expression.

## Eval
```
function Eval(e, a) {
  var A = cx;
  if (!e) return e;
  if (e > 0) return Assoc(e, a);
  if (Car(e) == kQuote) return Car(Cdr(e));
  if (Car(e) == kCond) return Evcon(Cdr(e), a);
  return Gc(A, Apply(Car(e), Evlis(Cdr(e), a), a));
}
```

`Eval` takes 2 arguments
1. `e` then expression to be evaluated
2. `a` the environment map (an *alist* in this code)

`Eval` picks off the low-hanging fruit in 4 sequential steps, then returns a value *and* performs a cleanup (`GC`) in case any unused leftovers remain on the stack.

Note that McCarthy's Lisp 1.5 uses a brute-force cleanup technique - called `mark and sweep` - whereas Tunney's GC relies on the use of pure FP (Functional Programming).  Instead of scanning all of memory, like mark-and-sweep, Tunney's GC knows that everything, but everything, operates in a stack-like manner - there is no heap and no explicit mutation and no Random Access (RAM) behaviour.  This FP-purity makes it very much cheaper to implement a GC cleanup than a full-blown mark-and-sweep.  In this case, `Eval` only needs to clean up its own stack, knowing that all other invocations of `Eval` and `Apply` clean up their own messes, too.  Written in assembler, Tunney's GC is only 40 bytes long and touches only a few memory locations, whereas mark-and-sweep needs to stop the world and visit *every* memory location (and worse).

`Eval` checks for 4 conditions in sequence
1. if `e` is *nil* then, return *nil*
2. if `e` is an *atom*, look up its value in the environment and return that value
	- a "trick" is used to test if `e` is an atom or a list
	- `e` is actually just an index into memory (a "pointer") and the layout is arranged in such a way that *all* atoms have an index >0, while *all* lists have an index<0 and *nil* has an index of exactly 0
1. otherwise, `e` must be a list (there are only 2 choices - list or atom - and we weeded out all atoms in the previous test)
	3. if `e` is a list with the word (atom) "`quote`" as the first item, return the second item in the list
	4. if `e` is a list with the word (atom) "`cond`" as the first item, evaluate the rest of the list as a *conditional* using the helper function `Evcon`
2. if all of the above fails, 
	1. peel off the first item of the list (this will be the function)
	2. loop through the rest of the items and `Eval` them (they are arguments to the function), using the helper function `Evlis`
	3. call `Apply` to apply the function again the list of actual values (evaluated arguments)
		- note that the whole process is incestuously recursive, so any of the arguments might, also, be function calls (recursively) - the way that the code is written (mutual recursion) handles all of that, regardless of how deep the process goes
	4. clean up (GC)
## Apply
```
function Apply(f, x, a) {
  if (f < 0)      return Eval(Car(Cdr(Cdr(f))), Pairlis(Car(Cdr(f)), x, a));
  if (f == kEq)   return Car(x) == Car(Cdr(x));
  if (f == kCons) return Cons(Car(x), Car(Cdr(x)));
  if (f == kAtom) return Car(x) >= 0;
  if (f == kCar)  return Car(Car(x));
  if (f == kCdr)  return Cdr(Car(x));
  return Apply(Assoc(f, a), x, a);
}
```

`Apply` works a lot like `Eval`.  It checks for low-hanging fruit and/or punts back to `Eval`

Basically, `Apply` checks if the function matches one of 5 hard-coded built-ins.  

The first test in `Apply` determines if `f` is a list, and, therefore, is not any of the built-ins.  In that case, it pushes mappings onto a new environment and punts to `Eval`.  It uses the helper function `Pairlis`.

Note that `Car(Cdr(f))` extracts the 2nd item from the list `f`, and, `Car(Cdr(Cdr(f)))` extracts the 3rd item from the list `f`.

The first test weeds out all cases where `f` is a list.

After this first check, `f` must be an *atom*.  

The atom `f` is checked against 5 built-ins and, if that fails, then the default is to assume that `f` is a variable which contains a function or one of the built-ins.  In this case, we look up `f` in the environment map (`Assoc(f, a)`), then send its value and the given args back to `Apply`.

### Lambda
In Lisp, an anonymous function is a list of 3 items
1. the keyword "`lambda`" (i.e. the atom `lambda`)
2. a list of names of the parameters (each name is an atom)
3. the body of the function
	- normally, the body is a list of more - recursive - Lisp expressions
	- if the body is a single atom, then it needs to be one of the built-ins, else, the lookup will panic fail
		- actually, the code is written to conserve code space at the expense of checking. `Apply` will crash (loop indefinitely) if the lookup fails (i.e. the lookup returns *nil*)
			- this doesn't really matter for the use-case of Sector Lisp being used for bootstrapping (it's very low level systems code - you are expected to debug it and ensure that it is not buggy)

Given that an anonymous function is a list of 3 items, we can see that the first item - the `lambda` keyword - is just a flag.  When we write super-optimal systems code, we drop all error checks to save space.  In this case, we can write code that doesn't bother to check for the `lambda` flag, i.e. if the function is a list, then we assume that it must be a `lambda` list.  In general, ignoring error checks is not a good idea, but, that is the way that this code is written - it either runs or it crashes.  There is no debugger to help and there are no error checks, to save space. Computers are just machines - they do exactly what you tell them to do. If you tell the machine to do something stupid or wrong, it will do it. Compilers and type-checking try to the map HLL checked code into unchecked assembler code.  In the process, compilers weed out your mistakes before committing the code to assembler.  This can only be done if you twist the HLL to design it to be checkable.  This is called *static type checking*.  You can, also, wire checks into the low-level code so that every operation is checked - at runtime - before it is executed, in order to prevent crashing.  This is called *dynamic type checking*.  Dynamic type checking prevents crashes at the expense of your knowing, definitively, that *all* of the code is sound and won't cause crashes (dynamic type checking only checks types that are encountered, but, cannot check the code that isn't encountered).  Static type checking prevents crashes by preprocessing the code, and, it allows unchecked assembler code to be used - after the code has been checked - the save on space and speed.  A pitfall of static type checking is that the program must follow a set of rules which restrict what can the machine can do.  In essence, static type checking makes the process of Design less efficient with the trade-off that the final code runs faster, whereas dynamic type checking allows more degrees of freedom during Design, allowing the machine to perform more kinds of operations, with the trade-off that you can never be sure if some other, untested, path through the code will cause a crash.

It is currently mis-believed that static type checking guarantees that programs are not ad-hoc.  In fact, the process of discovering which restrictions are necessary to allow for static type checking, is ad-hoc and leads to unexpected *gotchas* further down the road.  A glaring example of such failure is the Mars Pathfinder disaster.  The Mars Pathfinder failed in a very inconvenient and expensive manner.  The cause of the failure was only later addressed by slapping a band-aid, called "priority inheritance", onto the tower of restrictions that allowed continued use of the programming techniques.  

Ad-hoc-ness will always be with us, regardless of the language used.  For example, the word "robust" applies to only a small part of the overall process and should not be misconstrued to mean that the overall process is robust, even if static type checking is used.
## Cons Cells

![cons cells](/diagrams/Lisp%20Eval%20and%20Apply-2023-12-12-1659.svg)
## Evlis
Loops through a given list and `Eval`s each item, using the supplied environment (the 2nd parameter) to lookup variables.

Returns a list of values.

`Evlis` is used for making a list of actual arguments for a function call.

`(evlis '(a b c) '((a . 1)(b . 2)(c . 3))` returns `(1 2 3).
## Pairlis
A zipper.  

`Pairlis` takes two arguments
1. a list of names (atoms)
2. a list of values.

It returns a Dictionary (an alist in this particular case) of {name X value} items.

An *alist* is a caveman Dictionary.  An *alist* is a list of cons cells.

The *car* of each cell is a name (atom).

The *cdr* of each cell is a value.

The result is pushed onto the current environment and extends the environment for further calls to `Apply`.
`(evlis '(a b c) '(1 2 3)` returns `((a . 1)(b . 2)(c . 3))`

aside: `(1 . (2 . (3 . nil)))` prints, shorthand, as `(1 2 3)`
## Evcon
`Evcon` is used to evaluate a conditional.

`Evcon`takes 2 arguments
1. a list of pairs {test X body}
2. an environment.

`Evcon`loops over the list of pairs (first argument) and `Eval`s the first expression in each pair, in order.  When a test expression (first of pair) `Eval`s to anything but *nil*, the body expression (second of pair) is `Eval`ed and its result is returned as the result of the conditional.  Looping stops after the first successful {test X body} pair is found.

Looping, of course, is done via recursion, where the list of pairs is shrunk down on each successive iteration.  This is done by effectively popping the first pair off of the list before recurring further.  In this case, popping doesn't actually mutate the list, but, `(cdr ...)` is used to make the argument into a smaller list (by 1 element).  The "loop" stops when the list of pairs is empty (*nil*).  That's the typical pattern for recursion - 
1. test for the termination case (empty list)
2. if not empty, proceed to do something with the top item before diving further down with a shortened list.
## GC - Garbage Collection

[TBD]

https://youtu.be/baRH_d0Wnhc

