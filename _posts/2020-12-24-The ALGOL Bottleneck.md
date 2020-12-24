Title: The ALGOL Bottlenck  
Author:

# Introduction #

## von Neuman Bottleneck ##

* The von Neumann architecture is a hardware architecture.

* von Neumann architecture uses a single bus for both, code and data.

* This architecture gives rise to something called the von Neumann Bottleneck.
	
* The problem is that code cannot execute while data is being transferred.
	
* Other hardware architectures repair this problem by using multiple buses.  
	
* Other architectures allow asynchronous (at the same time) transfer of data and code.

## Can Programming Be Liberated... ##

* famous paper "Can programming be liberated from the von Neumann style?: a functional style and its algebra of programs"[^fn1] 

* proposes the idea that the von Neumann hardware architecture translates directly into the software domain




## ALGOL Bottleneck ##

* Software has yet another bottleneck that doesn't involve the underlying hardware

* I call this the ALGOL Bottleneck
	
* Lack of asynchrony

# Fiction vs. Reality #

## Fiction: Libraries are Independent ##





How Programmers Think About Libraries

![][Libraries-Fiction]



## Reality: Libraries Share A Global Variable ##

How Libraries Actually Work

![][Libraries-Reality]


[Libraries-Fiction]: Libraries-Fiction.png width=250px height=387px

[Libraries-Reality]: Libraries-Reality.png width=250px height=388px

[^fn1]: https://dl.acm.org/doi/10.1145/359576.359579
