## Odin Memory Layouts

This essay contains a walk-through of five experiments and diagrams that show how the Odin compiler lays out data in memory.

I aim for easier readability, and, don't aim for precision.  My description is loosey-goosey and may contain minor details that are factually incorrect.  My goal is to give an overview of how memory is laid out, and to avoid discussing too many details that might confuse the first-time reader.  Hopefully, this approach allows the reader to generally understand what is going on and to fill in and seek out more details as desired.

Hopefully, the first-time reader can start by just looking at the diagrams.  The reader can dig deeper into the details by reading the surrounding text.

The memory layout for the complete program is shown in *Block 5*. That diagram contains lots of details and arrows.  I hope to build up an explanation of that diagram in four simpler stages - *Blocks 1 through 4*.

The Odin code can be found in the repository listed in the Appendix. The reader is encouraged to download and run the code while reading this essay.
## Block 1
```
    // BLOCK 1
    cs := "TARVY"
    fmt.printf ("%v\n", typeid_of (type_of (cs)))
    fmt.printf ("%v\n", raw_data (cs))
    fmt.printf ("%v\n", len (cs))
    fmt.printf ("%v\n", &cs)
```

- Create a constant string containing a prime number of bytes.  
- I choose some arbitrary 5 bytes - in this case the first 5, upper case, letters in my surname "TARVY".
	- I choose a prime number in the hopes that I won't get fooled by alignment and allocation optimizations.
- The 5-byte string is assigned to a local variable named *cs* (the plural of *c*, where *c* is a short-hand for *character*).
- A *string* is an Odin datatype consisting of 2 quadwords
	1. a pointer (8 bytes - one quadword)
	2. a length (8 bytes - a second quadword)
		1. a "Word" is 2 bytes long, hence, a quadword is 4 x 2 bytes long, i.e. 8 bytes
- I print out (`fmt.printf`)
	- The type id of *cs*
	- The first quadword of *cs* - the pointer to the array of bytes "TARVY"
	- The second quadword of *cs* - the length of the string "TARVY"- 5 in this case.  This length is known at compile time and can be hard-coded into the code by the compiler.  In general, the length cannot be known until run-time, so hard-coding is not always possible.  The compiler is built to look out for simple opportunities to hard-code details.
	- The hex address of *cs*.

The program prints:

```
string
0x10CCDB76C
5
0x7FF7B32680C8
```

### Type ID
The type id is some binary code that the runtime understands and translates to "`string`" when printing.

### Pointer to the Array of Bytes
The array of contiguous bytes - "TARVY" - is at location 0x10CCDB76C.  

#### Allocation
There are 3 places where bytes can be stored:
1. The stack (RAM)
2. The heap (RAM, again)
3. ROM - immutable memory.  Code is also stored in ROM.
![](/diagrams/2023-10-02-Odin%20Memory%20Layouts%202023-10-02%2022.39.50.excalidraw.svg)

The stack most often starts at the "top" of memory and grows inwards from 0x7FFxxxxxxxxxxxxx toward 0x00000000000000000.

ROM usually starts at low memory, 0x10xxxxxx and grows upwards towards high memory.

Heap is usually located somewhere in the middle.

The actual, detailed locations are figured out by the compiler.

Here, we see that the array of bytes for the constant string "TARVY" is probably stored in ROM, at a low location 0x10CCDB76C.

CPU registers are simply RAM locations.  These bits of RAM are special, in that they are really, really fast to access.  It costs a lot of money (and head-scratching) to make really, really fast RAM, so there is a limited supply of *registers*, and, the registers are shared by all software installed on the same CPU.

RAM is just an array of contiguous bytes.  An *address* is simply an index into the array.  It is easy to use indices starting at 0 and incrementing upwards, and, to use addresses starting at the very top, 0x7FFFFFFFFFFFFFFF and incrementing downward.  Note that we use a hexadecimal numbering system 0-9, A-F (0-15 in decimal), since this is a convenient way to talk about integer indices for binary RAM locations.  We use the prefix "0x" to remind us that the integer is written in hexadecimal form.  Other reminders, like "%" are used, too.  It depends - read the docs, if you care.

So, we can easily put things into low memory - 0x0000000000000000 - and high memory - 0x7FFFFFFFFFFFFFFF.  We put "ROM" in low-ish memory and we put "stack" in high-ish memory.  We put "heap" somewhere in the middle.

The very-highest chunk of address space 0x8000000000000000 to 0xFFFFFFFFFFFFFFFF is reserved for special software, like the operating system software.
#### Garbage Collection

Allocation is determined by the compiler.  The programmer and the compiler determine where the bytes are to be stored and how that storage is reclaimed, if necessary.

Stack-based variables are mutable and their storage are automagically reclaimed when the Stack is popped. The stack pointer is stored in a shared variable - a register - which usually has a name with "SP" in it, like the name "%RSP".  The Stack Pointer simply holds the address - a RAM index - of some location in RAM.  Note that "popping the stack" by simply changing the integer stored in the SP register doesn't actually clear the old stuff out of memory.  This can lead to bugs, but, the convenience and speed of using a Stack Pointer is - by far - better than anything else, so, we do this, a lot.  Pushing and popping the stack is supported by operations that are hard-wired into the hardware and can be very fast.

![](diagrams/2023-10-02-Odin%20Memory%20Layouts%202023-10-02%2022.22.37.excalidraw.svg)
%%[🖋 Edit in Excalidraw](diagrams/2023-10-02-Odin%20Memory%20Layouts%202023-10-02%2022.22.37.excalidraw.md), and the [dark exported image](diagrams/2023-10-02-Odin%20Memory%20Layouts%202023-10-02%2022.22.37.excalidraw.dark.svg)%%

Heap-based variables are mutable and are stored somewhere - anywhere - in RAM.  There is no hardware support for cleaning up memory in the heap, and, random-access clean-up can leave unused holes peppered throughout the RAM.  The C programming language supplies library functions *malloc()* and *free()* to create variables in the heap.  Odin tries to help programmers manage the HEAP better than C does, using built-in language constructs like `new` and `make`, etc.  Read the docs if you want more detail. 

ROM-based variables are not mutable - i.e. they are *immutable* - and can never be freed. If the compiler can figure out that some data is known at compile-time and will never need to be changed, that data is stuffed into ROM and remains there "forever".
### Length

The length of the string "TARVY" is 5 bytes.  In the general case a length can be as large as a whole quadword.

In this case, we use up a whole quadword to store a small integer, 0x0000000000000005.

### Local Variables

The variable *cs* is declared to be "local" to the function *block1()*.  In this case, the *cs* variable is stored on "the stack" and garbage-collected automagically when the Stack Pointer is popped.  The variable *cs* is said to be *scoped* and only exists as long as the function exists.  The Stack Pointer is decremented ("push") when the function is entered and the Stack Pointer is incremented ("pop") when the function quits.

In this case, the address of *cs* is printed out as `0x7FF7B32680C8` which looks like a Stack address.  The address contains only 6 bytes, not 8 bytes.  Maybe the address space for a user program extends from 0x100000000000 to 0x7FFFFFFFFFFF instead of the full 0x0000000000000000 to 0x7FFFFFFFFFFFFFFF.  I'm not sure.    This looks plenty big. If you really want to know, this will require further investigation .  Note that most modern hardware contains memory mapping hardware ("MMU"s) that can make discontiguous blocks of memory look like they are contiguous as far as the user program is concerned.

### 4 Local Variables

In the whole `main` program, four (4) local variables are declared
1. cs
2. clonedcs
3. pany
4. pdatum

Block 1 uses only the first variable *cs*.  

The compiler, though, scans the whole *main* function and figures out how many local variables will be needed.

The compiler creates slots on the stack for all four variables.  Each slot is made to correspond to the size of the variable declared in the code.

1. *cs* is declared to be a *string*.  In Odin, strings are 16 bytes long - 2 quadwords.  The first quadword is the address (called a "pointer") of a block of bytes that contains the bytes that make up the string.  In this case, the bytes are "TARVY".  The compiler places those 5 bytes in ROM.
2. *clonedcs* is also declared (later) as a *string*, hence, two quadwords are reserved for it.
3. *pany* is declared to be a pointer - `"^"` in Odin lingo.  A pointer is only one (1) quadword long.
4. *pdatum* is, also, a pointer.  One quadword is reserved for it.

The stack is bumped by `2+2+1+1` quadwords, which is 6 X 4 which is 24 bytes.  The Stack grows from high addresses to lower addresses, so the bumping is done by subtracting 24 from ISP.

Odin guarantees that all variables are initialized to their zero value.  After creating code for bumping the Stack, the Odin compiler creates code to zero out the 24 bytes.

On the other hand, the C language does *not* guarantee that variables are zeroed out, hence, a C compiler would only generate code to bump the Stack, but would generate no extra code to zero out the variables.  Initially, the variables contain whatever garbage has been left on the stack, in those memory locations.  In buggy programs, this sort of behaviour causes mysterious-looking bugs, depending on *when* the function is called and what junk is left on the stack at that time. The junk found on the stack depends on the dynamic call sequence of the program at runtime.  For example if functions f1(), f2() and f3() are called at runtime, f3() "sees" whatever junk was left over by f2() (and, maybe f1()), whereas if function f3() is called after function f4() is called, f3() "sees" f4's left-overs.

![](/diagrams/2023-10-02-Odin%20Memory%20Layouts%202023-10-03%2005.24.12.excalidraw.svg)


It turns out that leaving stuff on the stack can pose a security risk, also.

Odin doesn't allow for any of the above.  Odin zeroes out the variables, at the expense of creating extra code.
### Temporary Variables

Occasionally, the way that the code is written causes the compiler to calculate intermediate results.  

The compiler needs to save those results *somewhere*.

For example, before calling a regular function, the compiler needs to generate code for each parameter to the function.  Let's say that the compiler sees a function call like `f(g(x),h(y))`.  It needs to calculate `g(x)` and put the result somewhere.  Then, the compiler needs to calculate `h(y)` and put the result somewhere.  Finally, the compiler restores the two intermediate results and passes them to function `f(...)`.

Ideally, the compiler will stuff the results into some unused CPU registers.

Often, though, aggressive compilers use every register possible.  This usually means that there are no unused registers available for saving temporary results.

Sometimes, the temporary results don't fit into registers, e.g. when the results are too big (contain too many bytes) and/or are layered in some way (containing structs that contain structs).

In such cases, the compiler pre-allocates empty slots on the Stack and uses the slots when it needs to save temporaries.  The compiler figures this out on its own - the Odin source code doesn't specify when this is necessary.

You can only see this kind of thing happening by examining the assembler code created by the compiler, but, then, who bothers to look at the assembler? (A: only compiler-writers look at the assembler when they are debugging the compiler(s) that they are writing).

### Memory Layout

![](/diagrams/stringclone-block 1.drawio.svg)
## Block 2
```
    // BLOCK 2
    fmt.printf ("\nBLOCK 2\n")
    clonedcs := strings.clone (cs)
    fmt.printf ("%v\n", typeid_of (type_of (clonedcs)))
    fmt.printf ("%v\n", raw_data (clonedcs))
    fmt.printf ("%v\n", len (clonedcs))
    fmt.printf ("%v\n", &clonedcs)
```

Block 2, builds on the work done in Block 1.  We clone the string "TARVY" from ROM to heap.  We stuff the cloned heap variable into local variable called *clonedcs*.

The diagram shows this process in two steps.
1. First, the clone is created in HEAP.  The 5 bytes are copied and a *string* variable, of two quadwords, is created in HEAP.  The pointer in the *string* variable contains the address of the copied five bytes.  The length portion of the *string* variable contains the hard-coded integer "5".
2. Next, the HEAP variable is copied - *by value* - into the Stack at the location called *clonedcs*.  The pointer to the HEAP bytes is copied into the Stack.  The integer, 5, is copied into the stack.

The result is that there are two (2) variables that point to the same five bytes.  This is called *aliasing*.  One variable remains in the HEAP and the other variable is located in *clonedcs* on the stack.
### Memory Layout
![](/diagrams/stringclone-block 2.drawio.svg)
## Block 3
```
    // BLOCK 3
    fmt.printf ("\nBLOCK 3\n")
    pany : ^any = new (any)
    pany^ = clonedcs
    fmt.printf ("%v\n", typeid_of (type_of (pany.(string))))
    fmt.printf ("%v\n", raw_data (pany.(string)))
    fmt.printf ("%v\n", len (pany.(string)))
    fmt.printf ("0x%p\n", &pany)
```
Block 3 goes further by creating a pointer to a variable of type *any*.  This is a type found in the Odin language, and, cannot be found in most programming languages that were created before the Odin language was created.

A variable of type *any* consists of two quadwords (16 bytes total).  The first quadword contains a raw pointer to another variable.  The second quadword contains a binary (integer) code that specifies the type of the variable being pointed to.

In days of yore, use of the datatype *any* was called *dynamic typing*.  This is what happens in languages like JavaScript and Python, etc.  The compiler doesn't weed out typing information, it attaches the typing information to the variable(s).  At runtime, the program can use the typing information to perform introspection among other things.

In this case, we create the *any* variable in HEAP.  We keep a pointer to it on the Stack in a location called `"pany"` (I use "p" as a prefix to remind me that the variable is a pointer).

A *pointer* is a single quadword.  In this case, the pointer - called *pany* - is stored on the Stack.  It points to a variable (no name) consisting of two quadwords in the HEAP.  That variable contains yet another pointer to a *string* variable, and, that variable contains yet another pointer to five bytes in the HEAP. 

Oy vey.  I certainly need a diagram to keep this all straight...

### Memory Layout
![](/diagrams/stringclone-block 3.drawio.svg)
## Block 4
```
    // BLOCK 4
    fmt.printf ("\nBLOCK 4\n")
    pdatum : ^Datum = new (Datum)
    pdatum.data = strings.clone (cs)
    fmt.printf ("%v\n", typeid_of (type_of (pdatum.data.(string))))
    fmt.printf ("%v\n", raw_data (pdatum.data.(string)))
    fmt.printf ("%v\n", len (pdatum.data.(string)))
    fmt.printf ("0x%p\n", &pdatum)
```

Block 4 continues to build up the complexity of the code.  Here, we create a different kind of variable, of type *Datum*.  We stick that variable into the HEAP, and, we keep a pointer to it, called *pdatum* on the STACK.

I've culled the code to minimize the contents of the *Datum* datatype.  After culling, it turns out that the *Datum* datatype is two quadwords long.  The *Datum* datatype contains one field - of type *any*.  The field is called `"data"`.

The fact that the culled version of *Datum* is the same size as the *pany* variable in Block 3 is merely a coincidence.

The *.data* field of *Datum* is of type *any*.  We remember, from above, that an *any* variable is two quadwords long, and, contains a pointer and a secret code.  We see this as the red blob in the diagram below.  Note that, at this point, the HEAP contains two (2) variables of type *any*, one coloured red and the other coloured purple.  The red variable has a dotted line around it to remind me that the red portion is actually part of a *Datum struct*.
### Memory Layout
![](/diagrams/stringclone-block 4.drawio.svg)
## Block 5
```

    // BLOCK 5
    fmt.printf ("\nBLOCK 5\n")
    pdatum5 := f (cs)
    fmt.printf ("%v\n", typeid_of (type_of (pdatum5.data.(string))))
    fmt.printf ("%v\n", raw_data (pdatum5.data.(string)))
    fmt.printf ("%v\n", len (pdatum5.data.(string)))
    fmt.printf ("0x%p\n", &pdatum5)
}

f :: proc (cs :string) -> ^Datum {
    pdatum5 : ^Datum = new (Datum)
    pdatum5.data = strings.clone (cs)
    return pdatum5
}
```

The final test is almost like that of Block 4, except that the *Datum* variable is created in a function (`f`) and is returned to `main`.

The memory layout works out to be the same as that in Block 4.
### Memory Layout
![](/diagrams/stringclone-block 5.drawio.svg)
## Appendix - Code Repository

## Appendix - Contact Me
email: paultarvydas@gmail.com

I would be glad to answer any question to the best of my abilities and available time.  No question is "too stupid" to ask.

In fact, feedback will help me improve the readability of this essay...
## Appendix - See Also

## See Also
### Blogs
[blog](https://guitarvydas.github.io/)

[obsidian blogs](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx-)

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
