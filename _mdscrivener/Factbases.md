Title: Factbases  
Author:

# Factbases #

The trick to automating anything in software is to find a way to normalize the information.

We discovered how to normalize code very early on - we used a notation called assembler.

Assembler is code represented as triples - relation, subject, object.

For example

MOV R0, R1

is a triple.  The relation is MOV.  The subject is R0.  The object is R1.

If the idea of triples sounds familiar, it's because you've already heard of it.

XML is triples[^fn1].  The Semantic Web is triples.

So, what is the normalized format of data?

Triples!

We want to put data into the form: relation, subject, object.

Conveniently, this already exists.  It is a function of two parameters:

relation(subject,object);

or, 

fn(id,x);

Why is this a Good Thing?  

Well, because we impose no structure on the data.  

If the data has no structure, then it is easy to parse (in an automatic manner).  

If the data has no structure, then it can be used for other kinds of things.  Things that the original programmer never thought of.

Note that organizing data into a data structure at compile time is just an optimization.  In the 1950's, it seemed like a good idea to preserve CPU power by pre-compiling data into data structures.

Today, CPUs are cheap and abundant, we can waste CPU time building data structures at runtime.  We don't have to worry about pre-compiling things.

How shall we waste CPU time?  

By performing exhaustive search.

By using backtracking.  Backtracking was verbotten in the 1900's, but no more.

I know, from experience, that I will be using PROLOG for doing exhaustive search.  So, I will put a period ('.') at the end of each function and call this a fact.

fn(id,x).

Caution: use the principles of Shuhari here.

Shu: don't expand the definition of "x" in the above.  It is one thing and one thing only.

For example, imagine that I have a rectangle R, with top-left (x,y) and a width, w, and a height, h.

In factbase notation, this becomes

rectangle(R,nil).
top_x(R,x).
top_y(R,y).
width(R,w).
height(R,h).

Resist the urge to do something like:

rectangle(R,[x,y,w,h]).

or

rectangle(R,nil).
top(R,[x,y]).
wh(R,[w,h]).

We will use CPU power[^fn2] to glean various relationships about the data.  In fact, one of the first relationships will be to create a bounding box for each rectangle (we will see this later).

CPU power is cheap.

Memory is cheap.

Don't waste brain power.

Don't try to predict the various ways in which data will be structured.[^fn3]

PROLOG already knows how to deal with triples of the above form.  

PROLOG knows how to search triples.  

You know how to search triples (loops within loops within …).  

It gets boring after a while.  

When it gets boring, automate.

Automation done before you know what you're doing is called premature optimization.

You can't know what you're doing unless you've done it manually several times[^fn4].

Corollary: premature optimization happens in anything that is built before the 3rd version.

Code is cheap, thinking is hard.

Code is cheap, experience is hard.



It is best to grow the factbase with new facts, rather than culling facts from the factbase.  This allows maximum flexibility during design.  Culling is just an optimization and should be left to Optimization Engineering.



Recap:

Code is normalized into triples, e.g. MOV R0,R1.

Data is normalized into triples, e.g. top_x(R,x).

Factbases are the normalized (triple-ified) form of data.

Further Reading:
see the Appendix for tools like gprolog, JS prolog, miniKanren, AWK.


[^fn1]: XML has too much syntax to be easily readable.

[^fn2]: exhaustive search

[^fn3]: Only tyrants tell you what to think.  Be free.  Let others be free.

[^fn4]: Fred Brooks says that you need to build something 2 times (and throw the results away).  Then, knowing what you are doing, you build it a 3rd time.