---
layout: post
title:  "Message Loops vs. Recursion"
---

Below is a diagram of a Component sending itself a message.

<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" width="296px" height="108px" viewBox="-0.5 -0.5 296 108" content="&lt;mxfile host=&quot;Electron&quot; modified=&quot;2021-06-28T21:18:06.704Z&quot; agent=&quot;Mozilla/5.0 (Macintosh; Intel Mac OS X 10_16_0) AppleWebKit/537.36 (KHTML, like Gecko) draw.io/12.4.2 Chrome/78.0.3904.130 Electron/7.1.4 Safari/537.36&quot; etag=&quot;RGmkN5JlPEFxX4L6vlWR&quot; version=&quot;12.4.2&quot; type=&quot;device&quot; pages=&quot;1&quot;&gt;&lt;diagram id=&quot;oRx2OKhrVAuivrzoCvYi&quot; name=&quot;message loop&quot;&gt;xVZNc5swEP01HNsxCLBzjB23OSSTzPhQ59SRkQC1MmKEMNBfX8ks346dpPH0ZPbtatG+t7vGQqt9+V3iNH4UhHLLmZHSQneW49j2zNc/BqlqZD4HIJKMQFAHbNgfCuAM0JwRmg0ClRBcsXQIBiJJaKAGGJZSFMOwUPDhW1Mc0QmwCTCfoj8YUXFb16xz3FMWxfDqhQeOPW6CAchiTETRg9DaQisphKqf9uWKckNew0t97tsr3vZikibqLQcevW3kHJhT3P98rp4e3J1Lb79AlgPmORS8gtuqqqFAijwh1GSxLbQsYqboJsWB8RZadI3Fas/BDfmoVLR89aJ2W77uGyr2VMlKh8ABZwGMQcvYPthFT4CG1bjHfROHQfOoTd3Roh+AmXew5ExYYsmEJp1HNyW9TBHO0rpTQ1YaWpch43wluJDHRIh4dEFcE8hZlGgs0MRR7VxmSorftBe6cHbI97VHs62e9BuZMqTpHvwcJeYjJebeRAl0Qgh0LSG8KetEjyuYQqpYRCLBfN2hy659DStdzIMQKSjyiypVwe7BuRJDvWjJ1Lb3/GJSffXAuish89GoGiPR5W77xkvf6A4dreZUXZ0p6bxgmgGRy4CeYQrBrsQyoupSa08bQFKOFTsM73FKzuPRWylx1QtIBUtU1sv8bICur1x31Fc3o9V1KX686kbxzr/Gz29GrVpX2DVuS9XHexlNlorI1fW2ShiGThC8aasQf+d719sqaLzf//dWcSdKTGVIyK35mjC8cZxlLBjtiJPzbn/avH90jnuUeicobbD3jftkftp/aFDUmY1S1OsKTp0ZROSMErkjzWseJokuz6Q2u0+tOrz7YEXrvw==&lt;/diagram&gt;&lt;/mxfile&gt;" style="background-color: rgb(255, 255, 255);"><defs/><g><rect x="127" y="47" width="120" height="60" rx="9" ry="9" fill="#ffffff" stroke="#000000" pointer-events="all"/><g transform="translate(182.5,70.5)"><switch><foreignObject style="overflow:visible;" pointer-events="all" width="8" height="12" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; font-size: 12px; font-family: Helvetica; color: rgb(0, 0, 0); line-height: 1.2; vertical-align: top; width: 10px; white-space: nowrap; overflow-wrap: normal; text-align: center;"><div xmlns="http://www.w3.org/1999/xhtml" style="display:inline-block;text-align:inherit;text-decoration:inherit;white-space:normal;">C</div></div></foreignObject><text x="4" y="12" fill="#000000" text-anchor="middle" font-size="12px" font-family="Helvetica">C</text></switch></g><ellipse cx="132" cy="77" rx="15" ry="15" fill="#d5e8d4" stroke="#82b366" pointer-events="all"/><g opacity="0.5" transform="translate(126.5,70.5)"><switch><foreignObject style="overflow:visible;" pointer-events="all" width="10" height="12" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; font-size: 12px; font-family: Helvetica; color: rgb(0, 0, 0); line-height: 1.2; vertical-align: top; width: 10px; white-space: nowrap; overflow-wrap: normal; text-align: center;"><div xmlns="http://www.w3.org/1999/xhtml" style="display:inline-block;text-align:inherit;text-decoration:inherit;white-space:normal;">in</div></div></foreignObject><text x="5" y="12" fill="#000000" text-anchor="middle" font-size="12px" font-family="Helvetica">in</text></switch></g><path d="M 257 77 L 287 77 L 287 7 L 87 7 L 87 66 L 114.63 66" fill="none" stroke="#000000" stroke-miterlimit="10" pointer-events="stroke"/><path d="M 119.88 66 L 112.88 69.5 L 114.63 66 L 112.88 62.5 Z" fill="#000000" stroke="#000000" stroke-miterlimit="10" pointer-events="all"/><ellipse cx="242" cy="77" rx="15" ry="15" fill="#fff2cc" stroke="#d6b656" pointer-events="all"/><g opacity="0.5" transform="translate(233.5,70.5)"><switch><foreignObject style="overflow:visible;" pointer-events="all" width="16" height="12" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; font-size: 12px; font-family: Helvetica; color: rgb(0, 0, 0); line-height: 1.2; vertical-align: top; width: 18px; white-space: nowrap; overflow-wrap: normal; text-align: center;"><div xmlns="http://www.w3.org/1999/xhtml" style="display:inline-block;text-align:inherit;text-decoration:inherit;white-space:normal;">out</div></div></foreignObject><text x="8" y="12" fill="#000000" text-anchor="middle" font-size="12px" font-family="Helvetica">out</text></switch></g><path d="M 7 88 L 115.03 87.63" fill="none" stroke="#000000" stroke-miterlimit="10" pointer-events="stroke"/><path d="M 120.28 87.61 L 113.29 91.13 L 115.03 87.63 L 113.26 84.13 Z" fill="#000000" stroke="#000000" stroke-miterlimit="10" pointer-events="all"/></g></svg>

Is the above diagram the same as recursion?

No.

With recursion, the loopback _returns_ a value to the caller.

In this diagram, though, C is an asynchronous software component (ASC).  It cannot process more messages until it has finished processing the message that it is currently working on.

So, in this case, C will see the message-to-itself only _after_ it has finished processing the first message.

The loopback arrow is like a queue.  

C can send itself messages, but the messages get queued up for later processing.

## Recursion and Stacks

Recursion implies the use of a _stack_.  

Recursive calls are processed immediately, suspending all work-in-progress.

## Asynchronous Software Components

ASC's never suspend work.  

If an ASC produces new messages, those messages are queued up at the receiver(s).

## Dispatcher

A Dispatcher invokes Components that have messages queued up.

The Components do not get to decide who runs next[^3].

Components create messages and leav it to the Dispatcher to decide which Component will run next.

[^3:] Note that with CALL/RETURN, the CALLer gets to determine who runs next, by CALLing a function.

## Distributed Computing (Internet)

Stacks are meaningless for distributed programming.

A _connection_ between two components can carry messages but it is not a _stack_ in the traditional sense

GPLs[^1] use stacks.

The internet does not use stacks.

[_Nodes on the internet might use GPLs and stacks, but the internet itself does not imply the use of stacks_.]

[^1:] GPL means General Purpose Language.

## CPS vs ASC

CPS means Continuation Passing Style, a technique that grew out of the use of first-class functions.

Continuations are tuples that contain data + control-flow.

CPS implies that control-flow is "changeable" and that control-flow is encoded in the Continuation.

ASCs, though, have exactly one control-flow. ASCs start running at the top _every_ time. [_If the programmer wants to program different control-flows, the programmer uses case statements._]

### Control Flow and the Internet

It doesn't make sense to send Control Flow across the internet.  

The best you can do is to send messages.  

The receiver reacts to the messages (maybe using a _case_ statement).

CPS includes control flow, hence, CPS is not a basic operation that can be used for distributed computing[^2].

[^2:] You can continue to cling to the CPS paradigm and fake it out using messages, though.

### RPC

RPC means Remote Procedure Call.

RPC _seems_ to do a CALL/RETURN over the internet.

This is actually faked out and is implemented by sending messages.  This kind of faking-out requires extra code and complexity and latency.

# See Also

[References](https://guitarvydas.github.io/2021/01/14/References.html)
[Table of Contents](https://guitarvydas.github.io/2021/05/14/Table-Of-Contents.html)

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
