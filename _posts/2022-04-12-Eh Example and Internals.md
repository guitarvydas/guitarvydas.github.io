---
layout: post
title:  "ė (eh) Example and Internals"
---

I describe the implementation of a very simplistic example using inner concurrency and a handful of diagrams.

The example is `cat`.  It copies the contents of a file to the console, character by character.  It, also, outputs each character on a port (unused in this simple example).

This document is a snapshot of my current progress in describing these concepts.

## Top Level

![Top Level of The Simple Example (cat)](/assets/cat![[cat.png]].png)

(obsidian:
![cat.png](file:///Users/tarvydas/Desktop/blogs/guitarvydas.github.io/assets/cat.png)
)

The diagram represents a very simple system with three (3) components total
- a Container
- two (2) Leaf components.

The Container is called `top`.

The Leaf components are called `read` and `write`.

`Top` runs the two leaves concurrently and routes messages between them.

`Top` is called (invoked) like a normal function and can return values like a normal function.  (In this example, `top` doesn't bother to return anything).

When `top` is invoked, it is passed two (2) parameters
1. the filename to be read
2. the filename to be written (which is ignored in this simple example, this example simply prints characters on the console and doesn't write them to a file).

`Top` injects these two filenames into the appropriate components and starts up concurrent dispatching.

How does `top` know when to stop dispatching?  One[^sev] of its children tells it to stop.  In this example, `read` invokes `conclude` when it hits end-of-file.

[^sev]: Or several of its children tell it to stop...

Note that the Leaf component `write` has an output `char` which is unused - `NC` (No Connection). 

`Write` does not know (cannot know) that its output `char` is not connected and, `write` continues to output characters to that output.  The *dispatcher* dumps messages coming from this pin on the floor (`pass` in Python lingo).

Note that `write` is never overwhelmed with too many input characters.  `Write` sends *request*s to `read` for each character.  [If we were concerned with efficiency, we might send big buffers of characters instead of single characters - but, that is left for Production Engineering to worry about].

## Ports

What is a Port?

A Port is a block (array) of data.

The data can be destructured into several sub-items, conforming to shapes that we call *types*.

All data on a single port arrives / leaves *at the same time*.

Ports, though, can fire at different times.

*Functions* in traditional programming languages, have exactly one (1) input port and (1) output port and cause the caller to *block* (implicit synchronization).  Such functions receive all of their data at once.  We call that input data "parameters" and imagine that they are separate items.  Such functions save up all of their output data and `send` it all at the same time in a single block.  If you know how compilers work, then you already know that parameters are stuffed into a global array (called The Stack) and are destructured by the callee. Likewise, compilers stuff all return data into the global array and the caller destructures the block when it wakes up again.  Compilers have different - aggressive - optimizing strategies, so the exact details might be different from what is described in the preceding.

Messages travel between ports.

## Blocking

Blocking is synchronization.

Blocking is usually thought to be controlled by the Operating System.

Blocking actually happens in two (2) places, voiding the principal of locality-of-reference.

Blocking is controlled by:
1. `CALL` and `RETURN` low-level, built-in CPU instructions
2. the Operating System.

Note that the Operating System needs to implement preemption (an epicycle) to yank blocking control away from processes which use the low-level `CALL` and `RETURN` blocking instructions.


## Synchronization Generalized

The general form of synchronization is to *ask* and *receive* via asynchronous messages.

The general form of synchronization can be seen in network protocols and in everyday life (e.g. interacting with other people).

Programmers tend to have difficulty with *multitasking* because they try to invert the natural order of life (where everything is asynchronous by default) and need to (re)-learn how to deal with such inversions of primary instincts. 

One *optimization* of synchronization is to use a global variable (The Stack) and the low-level, built-in `CALL` and`RETURN` instructions of the underlying CPUs.  In this case, the messages and state-machine protocols are implemented in hardware in an optimized manner.

## Boxes

Boxes, on a diagram, represent software components.

Concentric boxes represent synchronous components that allow inheritance (AKA scoping).

Separate boxes that communicate via messages on ports represent asynchronous components.

Every system consists of a single box that encloses other boxes.

Distributed systems appear not to have a single enclosing box, but, that is because we elide the top-level box and view only its innards.  For example, a robot is composed of many computers.  A robot is a single, stand-alone system, but we tend not to need to view it that way, and instead consider all of its parts as being separate entities.   We can change our mental "camera angle" to zoom-in and view the robot as a bunch of separate parts, or, we can zoom-out and consider the robot as a whole, e.g. when interacting with other robots and objects.  Being able to change our zoom factor allows us to avoid becoming overwhelmed with details and to describe (script) higher-and-higher level interactions. 

## Messages

A Message contains two fields:
1. an *etag*
2. *data*.

The *etag* is, currently, an implementation-dependent code (e.g. a number or a symbol or a string) that identifies the port (reason) that the message arrived on.

*Data* is a block of data.  The shape and size of the data depends on the component.  Akin to the concept of *implementation-dependent* size and shape, *data* is *component-dependent*.

The system does not define the size and shape of message data.  This cannot be known until the component has been implemented.  The Sender is responsible for sending appropriate data.  The Receiver is responsible for input validation.

*Future Consideration*: Can a type-checker / compiler / optimizer insert information into messages that help optimize the input validation phase(s)?

## How To Use

### Most Basic Usage

To run the basic tests:

`node test.js`

This should run three tests
1. read test using the Leaf `read.js`
2. write test using the Leaf `write.js`
3. container test using the Container `top.js` 


The read test uses `readwrapper.js` to run the `read.js` Leaf.

`Readwrapper.js` looks like a function / component to the outside world and can be called like a function.

`Readwrapper.js` creates a `read` component by using `read.js` and sends a test string into the `read` component.  In this example, the test string is `"text.txt"`, which is the filename of a small bit of text that is opened and read by the component.  `Readwrapper` creates fake entry points for the main programmatic features of a Leaf component and then punts (delegates) all calls to these entry points to the actual component that is being wrapped (i.e. `read`).

It is expected that `read` opens and reads the file and produces output messages.  In this - very simple - case, `read` opens and read the file character-by-character, producing one output message for each character.

The idea is that the `read` component `send`s these messages to other components for processing, but, in this case, we simply want to verify that `read` works as expected.

`Readwrapper` runs the `read` component, then dumps al of its outputs to the console for visual inspection.  This is a very low-level test.  As we build up larger and larger systems, we would write *test programs* to inspect the outputs instead of relying on manual inspection.

In this particular case, we expect `testwrapper.js` to output:
```
read ...
r outputs (r::[o]char:a:(rw::[i]req:true:.))
r outputs (r::[o]char:b:(rw::[i]req:true:.))
r outputs (r::[o]char:c:(rw::[i]req:true:.))      
```

Decoding this output:
- "r" is the name of the UUT `test.js`
- ``(r::[o]char:a:(rw::[i]req:true:.))`` is a message with tracing enabled
- tracing is read from left to right
	- the actual message comes first
	- followed by a nested trace of all messages that caused this message
	- `r::[o]char:a` says that the component "r" emitted an output message ([o]) with the etag `char` data `a`.
	- `:(rw::[i]req:true:.)` is a trace that says the the component "rw" (read wrapper) produced an input message tagged `req` and data `true` which was preceded by no other messages (`.`).

If we look at the source code for `read` (`read.js` / protoImplementation / handler), we see that it waits for a filename, then outputs one character message (`char`) every time it receives a `req` message. In normal usage, the `req` message would come from a downstream component, but in this test case, `testwrapper` generates (stub) `req` messages and injects these test messages into the `read` UUT with an appropriate etag (`req`).

The `read.js` component doesn't know (cannot know) where the `req` messages come from and simple responds to each one.

When `read.js` encounters an end-of-file condition, it invokes the `conclude` entry point which finishes the test and causes `testwrapper` to call `finish` and return.  In normal ("steady-state" usage), a Container would be calling `read` and the Container would supply a `conclude` entry point.  In this case, because we are testing `read`, the `conclude` entry point is supplied by `testwrapper`.

`Writewrapper.js` is built in a similar way.  We expect the write test to display the characters on the console and to send each of the characters as output messages.  The `write.js` component is like the `tee` command in UNIX® - it outputs each input character to two different places.

In normal usage, we would expect downstream components to use the output messages from `write.js`.  In this test case, however, we ignore the messages and manually inspect them as they are output.

`Topwrapper.js` is similar to the above, except that it uses a Container component and connects the output from `read` to the input of `write`. And, it connects the `request`
output from `write` to the `req` input of `read`.  N.B. the actual names of these etags is different - `request` vs. `req` - but neither Leaf component cares about this difference.  The routing table is set up in `top` and only `top` knows about the name differences.  An entry in `makeConnections()` explicitly wires the `w:request` output to the `r:req` input.

## Testing
The `readwrapper.js` code contains the term `uut`.  The term *uut* comes from the hardware-testing realm, meaning "Unit Under Test".  To test electronic circuits as they come off of the production line, one sets up a testing workbench and drops the UUT into the workbench.  The workbench drives inputs into the circuit and records outputs from the circuit.  A program (software) is used to check that the outputs conform to the expected results.  This technique works because electronic circuits are inherently asynchronous and carry no dependencies.  It is possible to test electronic circuits using simple stimulus-response techniques because the circuits are stand-alone (have no dependencies, except for very basic things like needing power from a battery or power supply).  Testers - ATE (automated test equipment) can do basic black-box testing.  Testers can also do white-box testing by poking probes directly into parts of the circuit using what is called a *bed of nails*. Test Engineers review circuit designs, before production, and suggest changes to the designs to insert *TP*s - Test Points - into the production circuits, to enable a layered approach to white-box testing. For example, first a black-box test is used to determine a GO/NOGO status for each production board.  Most boards don't fail and are shipped if they receive a "GO" status.  Boards that receive a "NO GO" status are tested further.  Electronic components can be expensive, so an attempt is made to repair "NO GO" boards.  The next layer of testing checks TPs to isolate problem areas.    This process continues to test deeper and deeper into the non-conforming circuits based on an ROI evaluation - "is it worth the time to delve deeper into the problem(s) in the hopes of repairing the board, or, is it cheaper to discard the board?".  Boards for which the problem issues are isolated are sent to a re-work station.  After being repaired, boards are put back into the production line for a new cycle of testing and shipping.

### Other Usage

Examine `test.js`.

It contains three (3) invocations of the test harness code. 

The final invocation `testContainer`

```
function testContainer () {
    var tw = require ('./topwrapper');
    var testHarness = new tw.TopWrapper ();
    
    //testHarness.tracing = true;
    
    testHarness.begin ('test.txt', 'test.out');
    testHarness.route ();

    while (!testHarness.done ()) {
        testHarness.step ();
        testHarness.route ();
    }

    testHarness.finish ();
}
...
testContainer ();
```
invokes `top` in three (3) major steps:
1. begin
	- `begin (*filename₁*, *filename₂*)`
	- followed by `route ()`
	- causes initialization of the `top` component, and,
	- routes any initial outputs to other components 
		- in this example, *filename₁* is sent to the `read` component, and,
		- *filename₂* is sent to the `write` component
		- as per the first (top-level) diagram
		- *future consideration*: it seems that `begin()` might be implemented using some `varargs` mechanism, but, for this example, we hard-code the two parameters into test.js
2. the main loop (dispatch)
	- test for completion
	- step the component (Containers try to step their children ; when no child has produced output, the Container declares itself to be "finished" and returns a flag that indicates whether there are messages on the Container's output queue)
3. finish.

## How To Modify

- begin by examining `top` and `topwrapper`
- create new components
	- for Leaf components, examine `read.js` and `write.js`
	- for Container componente, examine `top.js`

N.B. it is OK to leave inputs and outputs not connected *NC*.  This allows multiple use (reuse) of components in different situations.  It is not necessary to predict how a component will be used.  It is not necessary to parameterize a component for new usages (write a wrapper instead).

N.B. it is OK to create feedback loops of messages - a component sends itself a message, or, a chain of events causes a message to be sent back to the front of the same component chain.

N.B. it is possible to test components in a stand-alone manner.  Components have zero (0) dependencies on other components.  Components have well-define input and output signatures.  Components never contain hard-wired names of other components.

## Details of the Implementation

Each of the components is described by two uber-lists of attributes:
1. Signature
2. Implementation (prototype implementation).

When we define a component, we are defining a prototype.

When we want to compose a system using prototype components, we create *runnable* versions of each component (called *instances* in traditional programming).  

We can include more than one instance of the same prototype in a Container component.  Each instance is given a unique id (a graphical position) and sometimes provide *synonyms* for the id that are easier for humans to read (the machine doesn't care about the names, only humans do).  In general, we could provide more than one synonym for each component (e.g. a Greek letter vs. a phrase), but, in this simple example, we don't bother to do that (to keep things simple for human-oriented reading).

In fact, in this simple example, we use the name of the prototypes (`Top`, `read`, `write`) as the names for the runnable components.  This cheat works because - in this simple example - we have exactly one instance of every component.  To relate this concept to traditional programming, imagine "variable names" in programming languages.  Such names actually denote byte offsets for destructuring the data blocks.  In the extreme case, we use De Bruijn indices to elide human-readable names with stack offset indices.

We compose programs in a layered manner.  We create prototypes, then compose them (by "programming").  Since the composed components can be used in other systems, they act as prototypes for use in the other systems.  This layering is *fractal* and continues downward and upward ad infinitum[^turtles].

[^turtles]: "Turtles all the way down". https://en.wikipedia.org/wiki/Turtles_all_the_way_down.

## Signature

A signature contains three (3) pieces of information:
1. name
2. inputs
3. outputs.

```
var signature = {
    name: "read",
    inputs: [
        { "name": "filename", "structure": ["filename"] },
        { "name":"req", "structure":["req"] }
    ],
    outputs: [
        { "name": "char", "structure": ["char"] }
    ]
};
```

Each port has
- name
- destructuring information.

The destructuring information corresponds to what is called a *parameter list* in traditional languages.

Each port is asynchronous.  It does not make sense to describe all ports in a collapsed notation.

*Future Consideration*:  Does the destructuring information belong in the top-level signature, or, can it be demoted to a different level of description, or, described only in the implementation layers?  Currently, type-checkers want to "reach in" and know how each port is destructured.  Maybe type-checking can be moved to a separate pass (akin to, say, the Loader) and run in waves, checking only what can be checked with the given information and leaving breadcrumbs for future waves of checking?  A Component cannot be deemed to be *runnable* unless it contains no breadcrumbs.

## Prototype Implementation

Each Component runs but one `step` when commanded to do so by its Container.  The `step` must return `true` if any output was generated by the Component, or `false`
 if the Component created no outputs.

Each implementation contains attributes:
- name
- kind
- handler
- begin
- finish.

The `name` must correspond exactly to the name in the component's signature.

`Kind` is either `leaf` or `container`. 

`Begin` and `finish` are traditional functions that take one (1) parameter - *me* (like *self* or *this*).

`Handler` is a function of two (2) parameters
1. *me*
2. *message*

### Leaf

### Container

- children
	- each child prototype has
		- kind
		- destructuring
	- each child runnable (instance) has
		- unique name
		- unique runnable instantiation of kind
- connections
	- each connection has
		- sender
		- net name
		- list of receivers
- nets
	- name 
	- list of components on the net (key: "locks")
	
Nets are needed only in bare-metal situations - to lock all receivers before deliving message.  Semantics: one message must be delivered to all receivers "at the same time".

In implementations that use implicity synchrony (e.g. most programming languages and operating systems today), locking is not needed, since it is covered by the implicit synchrony.

### Wrappers

### Support Code

### Drakon Diagram

#### Step.Drakon
```
flowchart Try-component {
  start main
  skewer main {
    unless has-children try-self/1
    step-each-child
    unless child-produced-output try-self/2
    > produced-output/0
  }
  skewer try-self {
    : try-self/1
    : try-self/2
    run-self
    unless self-produced-output no-output/3
    > produced-output/0
  }
  skewer no-output {
    : no-output/3
    send no-output _
    > finished/0
  }
  skewer produced-output {
    send produced-output _
    > finished/0
  }
  skewer finished {
    end
  }
}
```

### Dia Diagrams

#### Handling.das

```
implementation deliverInputMessageToAllChildrenOfSelf (message)
      { find connection from me on port message.etag
        { lock connection
          { for every receivers in connection => dest
            { synonym params = {me, message, dest}
              { cond
                { dest.name != me
                  { #deliver_input_from_container_input_to_child_input <= params }
                }
                { dest.name == me
                  { #deliver_input_from_container_input_to_me_output <= params }
                }
              }
            }
          }
        }
        { orelse
          { pass }
        }
      }
```

#### Routing.das

```
implementation route
{ for every item in children of me => child
  { for every item in outputQueue of child.runnable => output_message
    { synonym message = output_message
      { find connection in me given child X message.etag => connection
        { lock connection
          { for every receivers in connection => dest
              { synonym params = {me, dest, message}
                { cond
                  { dest.name is not me
                    { @deliver_to_child_input <= params }
                  }
                  { dest.name is me
                    { @deliver_to_me_output <= params }
                  }
                }
            }
          }
        }
        { orelse
           { pass }
        }
      }
    }
    {@child.runnable.resetOutputQueue}
  }
}

sync deliver_to_child_input <= me, dest, message
   // map message for receiver
  { var input_message <= $i{{dest.etag, message.data} message}
    { lookup dest.name => receiver
      { @receiver.enqueueInput <= input_message }
    }
  }

sync deliver_to_me_output <= me, dest, message
  // map message for output
  { var output_message <= $o{{receiver.etag, message.data} message}
    { @me.enqueueOutput <= output_message }
  }
```

#### Find_connection.das
```
implementation find_connection (etag)
  { for every item in connections of me => connection
      { synonym sender = connection.sender
          { when all
              {
                  sender.name is me
                  sender.etag == etag
              }
              { -> connection }
          }
      }
  }

```

#### Find_connection_in__me.das
```
implementation find_connection_in__me (childname, etag)
  { for every item in connections of me => connection
      { synonym sender = connection.sender
          { when all
              {
                  sender.name == childname
                  sender.etag == etag
              }
              { -> connection }
          }
      }
  }

```

### Appendix - Github

[code on github](https://github.com/guitarvydas/duct)

### Appendix - Leaf "Read"
```
const runnable = require('./runnable');
const fs = require('fs');

var signature = {
    name: "read",
    inputs: [
        { "name": "filename", "structure": ["filename"] },
        { "name":"req", "structure":["req"] }
    ],
    outputs: [
        { "name": "char", "structure": ["char"] }
    ]
};

let protoImplementation = {
    name: "read",
    kind: "leaf",
    handler: function (me, message) {
        if ("filename" === message.etag) {
            me.filename = message.data;
            me.contents = fs.readFileSync (me.filename, 'utf8');
            me.cindex = 0;
        } else if ("req" === message.etag) {
            if (eof (me)) {
                me.conclude ();
            } else {
                me.send ("char", nextChar (me), me.name, message);
            }
        } else {
            me.errorUnhandledMessage (message);
        }
    },
    begin: function () {},
    finish: function () {}
}

function Read (container) {
    let me = new runnable.Leaf (signature, protoImplementation, container, "read");
    me.name = "r";
    me.filename = null;
    me.contents = null;
    me.index = null;
    return me;
}

exports.Read = Read;

// helper functions

function eof (me) {
    if (me.cindex > (me.contents.length - 1)) {
        return true;
    } else {
        return false;
    }
}

function nextChar (me) {
    let c = me.contents.substr (me.cindex, 1);
    me.cindex += 1;
    return c;
}
```

### Appendix - Leaf "Write"

```
const runnable = require('./runnable');

var signature = {
    name: "write",
    inputs: [
        { "name": "filename", "structure": ["filename"] },
        { "name": "char", "structure": ["char"] }
    ],
    outputs: [
        { "name": "request", "structure": ["request"] },
        { "char": "request", "structure": ["char"] }
    ]
};

var protoImplementation = {
    name: "write",
    kind: "leaf",
    handler: function (me, message) {
        if ("filename" === message.etag) {
            me.send ("request", true, me.name, message);
        } else if ("char" === message.etag) {
            process.stdout.write (message.data);
            me.send ("char", message.data, me.name, message);
            me.send ("request", true, me.name, message);
        } else {
            me.errorUnhandledMessage (message);
        }
    }
}

function Write (container) {
    let me = new runnable.Leaf (signature, protoImplementation, container);
    me.name = "w";
    me.filename = null;
    return me;
}

exports.Write = Write;

// This example code implements output to the console
// but is port-for-port compatible with output to a file (aka referential transparency)

// (in a future example, we will show how to create a 'write' part that wraps, both, 
//  file and console output ; this example is extra-KISS and does only one kind of output
//  to make the example a bare minimum)

```

### Appendix - Container "Top"

```
const handling = require('./handling');
const deliver = require('./containerDeliver');
const routing = require('./routing');
const runnable = require('./runnable');


const top = require('./top');
const read = require ('./read');
const write = require ('./write');

var signature = {
    name: "top",
    inputs: [
        { "name": "input filename", "structure": ["infname"] },
        { "name": "output filename", "structure": ["outfname"] }
    ],
    outputs: [
    ]
};

function begin (me, infname, outfname) {
    me.inject ("input filename", infname);
    me.inject ("output filename", outfname);
}

function finish (me) {
}

var protoImplementation = {
    name: "top",
    kind: "container",
    handler: handling.deliverInputMessageToAllChildrenOfSelf,
    route: routing.route,
    begin: begin,
    finish: finish
}       
    
function makeChildren (me) {
    var child1 = new read.Read (me);
    var child2 = new write.Write (me);
    return [
        {"name": "r", "runnable": child1}, 
        {"name": "w", "runnable": child2}
    ];
}

function makeNets (me) {
    return [
        {"name":"⇒₁","locks":["r"]},
        {"name":"⇒₂","locks":["w"]},
        {"name":"⇒₃","locks":["r"]},
        {"name":"⇒₄","locks":["w"]}
    ];
}

function makeConnections (me) {
    return [
        {"sender":{"name":"_me","etag":"input filename"},
         "net":"⇒₁",
         "receivers": [{"name":"r","etag":"filename"}]
        },                 
        {"sender":{"name":"_me","etag":"output filename"},
         "net":"⇒₂",
         "receivers": [{"name":"w","etag":"filename"}]
        },                 
        {"sender":{"name":"r","etag":"char"},
         "net":"⇒₃",
         "receivers": [{"name":"w","etag":"char"}]
        },                 
        {"sender":{"name":"w","etag":"request"},
         "net":"⇒₄",
         "receivers": [{"name":"r","etag":"req"}]
        }
    ];
}

function Top (container) {
    let me = new runnable.Container (signature, protoImplementation, container);
    me.name = "T";
    me.children = makeChildren (container);
    me.nets = makeNets (container);
    me.connections = makeConnections (container);
    me.deliver_input_from_container_input_to_child_input = deliver.deliver_input_from_container_input_to_child_input;
    me.deliver_input_from_container_input_to_me_output = deliver.deliver_input_from_container_input_to_me_output;
    return me;
}

exports.Top = Top;
```

### Appendix "ReadWrapper"

```
var read = require ('./read');
var message = require ('./message');

function ReadWrapper () {
    this.name = "rw";
    this.begin = function () {
        // this.args = ???
        uut.begin ();
    };
    this.finish = function () {
        uut.finish ();
    };
    this.isValidETagForUUT = isValidETagForUUT;
    this.isInputETag = isInputETag;
    this.send = function (etag, v) {
        if (this.isValidETagForUUT (etag)) {
            var m = new message.InputMessageNoTrace (etag, v, this.name);
            this.uut.handler (this.uut, m);
        } else {
            console.error (`invalid input message ${etag}`);
        }
    };
    this._done = false;
    this.conclude = function () { 
        this.container._done = true; 
    };
    this.done = function () {return this._done;};
    this.route = function () {
        this.uut.route ();
        if (this.tracing) {
            destructivelyDisplayAllOutputsForAllChildren (this);
        }
    };    
    this.step = function () {
        this.uut.step ();
        this.route ();
    };    
    this.uut =  new read.Read (this);
    this.children = [{name: "uut", runnable: this.uut}];
}

function isValidETagForUUT (etag) {
    if (this.isInputETag (etag)) {
        return true;
    } else {
        return false;
    }
}

function isInputETag (etag) {
    var inputs = this.uut.signature.inputs;
    return inputs.some (input => { return (etag === input.name); });
}

function destructivelyDisplayAllOutputsForAllChildren (me) {
    me.children.forEach (child => {
        var r = child.runnable;
        displayAllOutputs (r);
        r.resetOutputQueue ();
    });
}

function displayAllOutputs (child) {
    child.outputQueue.forEach (m => {
        console.log (`${child.name} outputs ${recursiveDisplay (m)}`);
    })
}

function recursiveDisplay (m) {
    if (m) {
        return `(${m.comefrom}::[${m.kind}]${m.etag}:${m.data}:${recursiveDisplay (m.tracer)})`;
    } else {
        return '.';
    }
}

exports.ReadWrapper = ReadWrapper;
```

### Appendix "WriteWrapper"

```
var write = require ('./write');
var message = require ('./message');

function WriteWrapper () {
    this.name = "ww";
    this.begin = function () {
        // this.args = ???
        uut.begin ();
    };
    this.finish = function () {
        uut.finish ();
    };
    this.isValidETagForUUT = isValidETagForUUT;
    this.isInputETag = isInputETag;
    this.send = function (etag, v) {
        if (this.isValidETagForUUT (etag)) {
            var m = new message.OutputMessageNoTrace (etag, v, this.name, undefined);
            this.uut.handler (this.uut, m);
        } else {
            console.error (`invalid input message ${message.etag}`);
        }
    };
    this._done = false;
    this.conclude = function () { 
        this.container._done = true; 
    };
    this.done = function () {return this._done;};
    this.route = function () {
        if (this.tracing) {
            destructivelyDisplayAllOutputsForAllChildren (this);
        }
    };    
    this.step = function () {
        this.uut.step ();
        this.route ();
    };    
    this.uut =  new write.Write (this);
    this.children = [{name: "uut", runnable: this.uut}];
}

function isValidETagForUUT (etag) {
    if (this.isInputETag (etag)) {
        return true;
    } else {
        return false;
    }
}

function isInputETag (etag) {
    var inputs = this.uut.signature.inputs;
    return inputs.some (input => { return (etag === input.name); });
}

function destructivelyDisplayAllOutputsForAllChildren (me) {
    me.children.forEach (child => {
        var r = child.runnable;
        displayAllOutputs (r);
        r.resetOutputQueue ();
    });
}

function displayAllOutputs (child) {
    child.outputQueue.forEach (m => {
        console.log (`${child.name} outputs ${recursiveDisplay (m)}`);
    })
}

function recursiveDisplay (m) {
    if (m) {
        return `(${m.comefrom}::[${m.kind}]${m.etag}:${m.data}:${recursiveDisplay (m.tracer)})`;
    } else {
        return '.';
    }
}

exports.WriteWrapper = WriteWrapper;
```

### Appendix "TopWrapper"

```
var top = require ('./top');
var message = require ('./message');

function TopWrapper (infname, outfname) {
    this.name = "tw";
    this.tracing = false;

    this.begin = function (infname, outfname) {
        this.uut.begin (this.uut, infname, outfname);
    };
    this.finish = function () {
        this.uut.finish (this.uut);
    };
    this.isValidETagForUUT = isValidETagForUUT;
    this.isInputETag = isInputETag;
    this.send = function (etag, v) {
        if (this.isValidETagForUUT (etag)) {
            var m = new message.OutputMessageNoTrace (etag, v, this.name, undefined);
            this.uut.handler (this.uut, m);
        } else {
            console.error (`invalid input message ${message.etag}`);
        }
    };
    this._done = false;
    this.conclude = function () { 
        this.container._done = true; 
    };
    this.done = function () {return this._done;};
    this.route = function () {
        destructivelyDisplayAllOutputsForAllChildrenAndDestroy (this);
    };    
    this.step = function () {
        this.uut.step ();
        if (this.tracing) {
            recursiveTraceOutput (this.uut);
        }
        this.route ();
    };    
    this.uut =  new top.Top (this);
    this.handler = this.step;
    this.children = [{name: "uut", runnable: this.uut}];
    this.route = function () {
        this.uut.route ();
    }
}

function isValidETagForUUT (etag) {
    if (this.isInputETag (etag)) {
        return true;
    } else {
        return false;
    }
}

function isInputETag (etag) {
    var inputs = this.uut.signature.inputs;
    return inputs.some (input => { return (etag === input.name); });
}

function destructivelyDisplayAllOutputsForAllChildren (me) {
    me.children.forEach (child => {
        var r = child.runnable;
        displayAllOutputs (r);
        r.resetOutputQueue ();
    });
}

function displayAllOutputsForAllChildren (me) {
    me.children.forEach (child => {
        displayAllOutputs (child.runnable);
    });
}

function displayAllOutputs (runnablechild) {
    runnablechild.outputQueue.forEach (m => {
        console.log (`${runnablechild.name} outputs ${recursiveDisplay (m)}`);
    })
}

function recursiveDisplay (m) {
    if (m) {
        return `(${m.comefrom}::[${m.kind}]${m.etag}:${m.data}:${recursiveDisplay (m.tracer)})`;
    } else {
        return '.';
    }
}

function recursivelyDisplayAllOutputsForAllChildren (me) {
    recursiveTraceOutput (me.uut);
}

function recursiveTraceOutput (me) {
    displayAllOutputsForAllChildren (me);
    me.children.forEach (childobject => {
        recursiveTraceOutput (childobject.runnable);
    });
}

exports.TopWrapper = TopWrapper;
```

### Appendix "Test.js"

```

function testRead () {
    var rw = require ('./readwrapper');
    var testHarness = new rw.ReadWrapper ();
    testHarness.send ("filename", "test.txt");
    while (!testHarness.done ()) {
        testHarness.send ("req", true); 
        testHarness.step ();
        testHarness.route ();
    }
}

function testWrite () {
    var ww = require ('./writewrapper');
    var testHarness = new ww.WriteWrapper ();
    testHarness.send ("filename", "test.out");
    testHarness.step ();
    testHarness.route ();
    testHarness.send ("char", "x");
    testHarness.step ();
    testHarness.route ();
    testHarness.send ("char", "y");
    testHarness.step ();
    testHarness.route ();
    testHarness.send ("char", "z");
    testHarness.step ();
    testHarness.route ();
}

function testContainer () {
    var tw = require ('./topwrapper');
    var testHarness = new tw.TopWrapper ();
    
    //testHarness.tracing = true;
    
    testHarness.begin ('test.txt', 'test.out');
    testHarness.route ();

    while (!testHarness.done ()) {
        testHarness.step ();
        testHarness.route ();
    }
}

console.log ();
console.log ('read ...');
testRead ();

console.log ();
console.log ('write ...');
testWrite ();

console.log ();
console.log ();
console.log ('top ...');
testContainer ();
```

## See Also

[ė - Concurrent Lambdas Working Paper 1](https://guitarvydas.github.io/2022/03/20/ė-Concurrent-Lambdas.html)

[ė - Concurrent Lambdas Working Paper 2](https://guitarvydas.github.io/2022/04/11/ė-Working-Paper-2.html)



[Table of Contents as of Dec. 01 2021](https://guitarvydas.github.io/2021/12/10/Table-of-Contents-Dec-01-2021.html)
[Blog](https://guitarvydas.github.io)
[Videos](https://www.youtube.com/channel/UC9EJr0nKHwadbHUtc5zHdmQ/videos)
[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Books](https://leanpub.com/u/paul-tarvydas.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" > 
</script> 
