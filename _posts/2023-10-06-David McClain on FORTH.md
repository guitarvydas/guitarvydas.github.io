[shared by permission]

I learned my Forth initially from Chuck Moore and Elizabeth Rather, who were contracted by us to build the control system for our brand new 100-inch Infrared Telescope (the world’s first!) atop Mt. Jelm, about 25 miles SW of Laramie, Wyoming. c.a.., 1976.  
  
The two of them spent a few weeks with us, and gave us 3 Astronomers (myself, John Hackwell, and Robert Gherz) our initial introduction to the system. In those days Forth was very easy to crash and hang, unintentionally. It had a mean time between reboots of around 10 minutes.  
  
Once I left the department, closing in on my Ph.D., I hired on as the scientist at the Multiple Mirror Telescope Observatory, atop Mt. Hopkins, about 50 miles South of Tucson, AZ.  
  
The MMT was the largest telescope in the world, at that time, with a 7 meter aperture, comprised of 6 x 72-inch mirrors arranged in a hexagonal pattern. Each of the 6 separate telescopes sent their light to a common focus in the center.   
  
So the pointing and tracking problem also had to include a beam combiner control system, in addition to running its Alt-Az mount.  
  
When I first arrived, the MMTO had budgeted around $10K for control computing and was using an ancient Tektronix calculator - I kid you not. An observatory with, at the time, a $10M annual operating budget using a $10K BCD calculator.  
  
So we scrounged up a couple of used Data General Nova 800 minicomputers. 16-bit wordsize, word addressable (not byte), and 32 kWords of core memory on them. The 800 designation came from its fantastic speed, at the time, with a Read-Modify-Write cycle time of 800 ns. Being core memory, every read was destructive and had to be re-written back into the core memory in a cycle.  
  
We kept one machine running by stealing parts from the other as they wore out. My partner in crime was John Montgomery who had come from Aerospace Corp and their 10 meter millimeter-wave radio telescope - which goes back to my very beginning in NYC...  
  
In NYC I began my graduate studies in Theoretical Astrophysics with Chi Yuan, who studied under C.C.Lin at MIT. We were doing gravitational spiral density wave theory to discover why galaxies formed spiral arms. And in support of our theories we also did observations of Carbon Monoxide in nearby spiral arms of our galaxy.  
  
Carbon monoxide can only form in protected cocoons in deep space, buried deep inside of clouds of dust and neutral hydrogen - to protect the fragile chemical bond from damaging ultraviolet light from all the stars nearby. As such, it exists in pockets at near 10 degK, inside the clouds of dust and gas.  
  
You can’t see neutral hydrogen H2 because it is a symmetric dumbell molecule and has no reason, quantum mechanically, to notify you when it changes its rotational state due to excitation or relaxation.  
  
But Carbon Monoxide, an asymmetric dumbell molecule, has a J 1 -> 0 transition line at 115 GHz as it moves from a state with 1 unit of angular momentum, back to zero angular momentum.  
  
Atop Pupin Hall at Columbia University there was a 1 meter Cassegrain dish radio telescope operating at 115 GHz to observe nearby CO lines. We used that telescope to map out the next-door Taurus Arm of our galaxy.  
  
At any rate, while I was just starting my graduate studies with Chi Yuan an upperclassman named Bob Dickman was just finishing his PhD in radio astronomy at 115 GHz. Bob had a falling out with his advisor, Pat Thaddeus at NASA Goddard Institute for Space Studies, just down the street from Columbia Univ., and Bob got his PhD on the condition that he not seek employment anywhere on the East Coast.  
  
So Bob found his way out to Los Angeles to Aerospace Corp and their brand new 10 meter millimeter wave radio telescope. This was a replica of the first one atop Kitt Peak, where Chuck Moore invented Forth to run that telescope.  
  
John Montgomery had studied Astrophysics at UCLA under Donald Clayton (?? - nucleosynthesis with William Fowler). John studied metal-poor stars in globular clusters in the visible spectrum. John came from Aerospace Corp where he worked with Bob Dickman. So we hit it off pretty well. I knew Bob from many long conversations in NYC - where we would talk about the intense study schedule of Astrophysics students as a possible distraction from who was paying us — the Defense Dept. — and why they were interested in our subjects...  
  
After NYC declared bankruptcy and Pres. Ford told them to go to hell, I decided that I better move along. As a lowly graduate student in Theoretical Astrophysics I was also a NYC City employee, right alongside Police and Fire men. Police and Firemen were being laid off. And surely we grad students would be next in line. Never mind - we were politically naive, and didn’t grasp that firing grad students would have nowhere near the political impact as place the city without police and firemen.  
  
But that urgency to skedaddle had me head out West to Wyoming where they were building the world’s first Infrared Telescope. A bit more blue-ward from 115 GHz. But I thought that maybe getting some more experimental physics under my belt would be a good idea.   
  
My professors in NYC pleaded with the stupid young man that I was, arguing that I should instead go to Yale or Princeton to continue my studies. Chi was headed off to a year at Westerbork in the Netherlands for a sabbatical at the time. I maybe should have gone with him… but I was young, stupid, and convinced of my need for experimental experience.  
  
At any rate, I began in Wyoming with a DEC PDP 11/40. Compared to the PDP 11, the Nova 800 looked quite primitive in its instruction set. But in reality, the Nova 800 was an early precursor to RISC architecture. It was truly a 3 register to memory system. You had to load from memory to the registers to perform anything, and then write back to memory. There was no register-memory operations except load and store.  
  
But it also had some special capabilities in the low 256 words. Some addresses were auto-incrementing, others were auto-decrementing, and still others were automatic indirection registers. So NEXT in Forth, for moving from one verb to the next was an indirect jump through location zero - a single word instruction.  
  
The entire inner interpreter of Forth was  
  
Inner:  
IP  )+ WP MOV  
WP )+ JMP  
  
where IP was our symbolic name for the Instruction Pointer register, WP was our Forth Word pointer - points to the body of the Colon def or CODE def, whose first word contained the address of the actual machine code for the kind of word that it was, and any data for the word immediately followed.  
  
Every word in Forth has a code pointer at its head (ignoring dictionary stuff), followed by data. Or in the case of actual Code words - machine code that performs some function - that data was the actual code of the function and the WP address simply pointed to its following word.   
  
Colon defs, variable defs, constant defs, all had W pointers at their heads that pointed to the code that performed their particular behavior.  
  
And every behavior or function machine code ended in NEXT which was a 0 ) JMP. The address of the inner interpreter was stored in location 0.  
  
The Forth system on the Nova 800 was blazing fast, compared to the CISC archecture of the PDP 11. The PDP 11 CISC gave us a whole lot more functionality, like byte and word addressing, and seemed to generate shorter code due to its register - memory architecture. But the RISC style of the NOVA 800, while taking more instructions, performed markedly faster. So I gradually came to love the DG NOVA machine.  
  
My first chore was to make us a Forth system for the MMTO. And one of my goals was to make it have a mean time between reboots of several days, instead of 10 minutes. I basically reverse engineered the Assembly code from our PDP-11 version in Wyoming and implemented my own take on it. I succeeded and we had our MMTO SuperForth.  
  
Using that SuperForth on our Nova-800 mount-control computer we tuned up the MMT telescope to point and track on the sky to better than 0.1 arcsec. That was phenomenal at the time. Many many long days. I used to fall asleep on the floor right under the computer at the observatory on Mt. Hopkins.   
  
It was such an arduous journey to reach the top of Mt. Hopkins that, instead of commuting 4 hours per day, I would just go up on Monday morning and come back to Tucson on Friday afternoon, spending the week up on the mountain working 24 hours per day till I dropped. My record was 40 straight hours working during a tuning run on the sky.  
  
After the first year at the MMTO, a new computer company offered a brand new NOVA-800 compatible, all solid state, and even faster computer with writable control store (!!). This was the Point-4 computer and it cost about $4,000 IIRC. I spent the better part of a year writing proposals and justifications to spend that $4,000 and get us a Point-4 computer. We finally got it but it was like pulling hen’s teeth at the University of Arizona. The MMTO was a joint project between Smithsonian and UofAz. I was a staff member at UofAz.  
  
After being frustrated with that ordeal just to spend a measly $4K, I heard about IBM hiring on at their new plant here in Tucson, and I applied. I got accepted, with a huge pay increase and no barriers to spending so little as $4K on a project.   
  
But it became clear to me that IBM was woefully in need of Forth. All the engineers were dependent on programmers from the IT Dept. Asking for a minor change to the control code for one of their machines took weeks to accomplish. And you know you need to iterate your ideas…  
  
So I taught a couple of the engineers about Forth, and then I had to go on tour to Yorktown Heights to discuss using Forth for their Robotics programs, and then to IBM Owego to their Federal Systems Division where they were building the first F/15 and AWACS computers. I taught them to use Forth to build a simulator for the new computer while they awaited its arrival, so they could program their control code while they waited.  
  
Before I left IBM, Forth had spread far and wide in the company among engineers. At the same time I was implementing a Forth system in town at a local machine shop to run his CNC machines. Frank, the owner of the shop, kept encouraging me to break away and go off on my own as a consultant Forth guy. He kept telling me that he had so much work that he could give me.  
  
… so I did… I walked away from my “career” at IBM to go off on my own. Then I called up Frank and told him, and he stammered about the work and said he was in kind of a financial bind. Everything up to that point with Frank had been gratis from me and a friend of mine working there at the shop on weekends, using an Apple II computer to replace the paper tape systems on the CNC machines.  
  
But there I was, fresh on the outside, just having left IBM with $1400 to my name in savings, and Frank wasn’t real. I’m sure you also have lots of similar stories…  
  
But I started Forthright Engineering, and developed HyperForth for the 68000. While at IBM the Motorola 68000 had just been released. A whole raft of new microcomputers based on the 16-bit 68K were coming out. And one company - Sage Computer - found my interest. They were based in Reno Nevada and it was almost affordable. My first Sage II computer had dual 5-inch floppy drives and 64 K of RAM. It ran UCSD P-System Pascal.  
  
I invented HyperForth on that machine. My next Sage was a Sage IV computer with a 20 MB hard drive and 1 MB RAM, and 6 serial ports so it could run several of us developers at once. HyperForth become a hit in the Forth world. I ended up getting the consulting job from Amiga to develop their first OS and BASIC Compiler — another convoluted story for another time.  
  
But that led to my writing HyperC a C compiler that had some early OO extensions, nested block structure, and some other goodies. HyperC was initially released on the Apple II computer running against a virtual 16-bit kernel that I furnished with it. Then HyperC was ported to the Sage IV and later the first Macintosh computer. A real 16-bit machine. That led to contracts with the VA Hospital system for automating their operating room anesthesia equipment banks, and eventually to the Black World of National Intelligence.  
  
And so we leave Forth behind and become infatuated with Smalltalk and later Lisp. I still use Smalltalk every day on my Kyma System here in the lab. But for the past 30 years I have been mostly Lisp, with a brief interlude using NML (my own vectorized ad-hoc math language based loosely on OCaml syntax but with dynamic vectorized typing). After leaving Hughes aka Raytheon Missile Systems, I gradually weaned away from NML back to Lisp.

---

Here is a Forth-like system written in Lisp. But with no absolute addressing. Everything good in Lisp comes along with it. Memory is just there when you need it, and you don’t need to know where it is. It just is.  
  
Where Forth uses native machine code for its CODE words, this one uses Lisp as its drop-down machine language. Which means you can do anything you want.  
  
It also includes a MetaForth which can cross-compile Forth source to another machine or another language. The example shows converting my Crescendo audio processing algorithm from Forth to C code for embedding in applications running on Windows computers.

[ForthRPL](https://github.com/dbmcclain/ForthRPL/tree/main)

---

# Appendix Github Repositories
[dbmcclain](https://github.com/dbmcclain?tab=repositories)

---
# Appendix - want to kill an early Nova 800 Forth system?  
  
0 0 !  
  
Store zero at location zero - an automatic indirection address. Location zero is also the address to the inner interpreter which is vectored by NEXT. This forms a hard tight loop and locks up the entire machine.  
  
- DM

---
# Appendix - Actors
My Actors system has gone through a deep metamorphosis as a result of bumping into this:

[fexpr the ultimate lambda](http://www.dalnefre.com/wp/2011/11/fexpr-the-ultimate-lambda/)

Dale Shumacher was a colleague of Hewitt a decade or more ago. Dale is not a Lisper, but his notion of asynchronous transactional Actors is stunning. 

In my Lisp implementation I am seeing approximately 20 M message transactions per sec, and each Actor is a tiny autonomous piece of pure functional code that handles just itself. No shared memory anywhere except in just one place in each Actor (its behavior pointer) which is tightly managed by the message dispatch.

So I have fully parallel concurrent programs capable of simultaneous execution of the same Actor body code, without using any shared memory nor locks. There are just 2 implicit locks in the communal message mailbox queue, and nowhere else. 

No need to even think about threads, locks, shared memory. It is a breeze to parallelize code. Just Actors sending messages to other Actors. Actors BECOME other behaviors as needed, and when a potential BECOME conflict arises, the loser is silently restarted as though it hadn’t yet seen the message.

Threads are there, as underlying Message Dispatch routines, feeding off the communal message queue. I run a pool of them, typically 8. But the same code runs perfectly fine with just one single Dispatch. You don’t ever have to think about these threads. They just are. And they enable parallel concurrency. But the system remains concurrent, even if only a single thread.

Transactional behavior means that no messages are sent, no behaviors are changed, unless the Actor body completes without error. There would be no visible effects in the program due to failed messages. Physically, you might see some memory being recycled due to tossed messages and new unused private Actors being created along the way. Messages to be sent are enqueued for dispatch at successful conclusion of the Actor bodies. And behavior changes cannot occur until successful exit.

Transactional Actors - small autonomous Actors in the system. These are amazing. And a breeze to interface with CAPI.

I have one program written to analyze audio album tracks for loudness statistics per EBU R128. This program, recast with transactional Actors scans my entire albums folder, recursively descending, and performing a parallel concurrent analysis of 4,000 tracks, covering about 12 hours of replay,  in just 2 minutes elapsed time on my M1 iMac.

The async socket layer was written in a single afternoon - almost trivial by comparison with imperative code with locks and threads. Messages can be sent to Actors on remote machines and the sender doesn’t even know that they are remote. There is no difference between sending a message to a local Actor and a remote Actor, except perhaps by elapsed time for some follow action to occur. 

Actors never expect a reply to any message. Messages are just sent asynchronously, perhaps along with the identity of the Actor to which a reply might be sent.

I think in the back of my mind how to adapt my GigaDSP system to these Actors. It would hugely simplify many aspects of that code. Not sure I’ll ever get around to it, since it already works so well for me.

- DM

… An Actor is nothing more than a wrapped (indirect) pointer to a behavior functional closure. That’s it. The closure contains code and its own local persistent data (persists until the possibly the behavior pointer is changed to exclude the data).

Functionally pure Actor behavior code means that local persistent data are never mutated. So parallel execution is perfectly fine. If you need to mutate some local data, you BECOME a fresh behavior with augmented copy of data. This means that parallel execution can’t be fudged in any way.

## Rebol
Rebol - Carl Sassenrath - one of the chief programmers on the Amiga project. Yes, we know each other. Part of that convoluted story on the Amiga.   
  
Carl was a bright young guy from Berkeley? or Stanford? But he was frustrated by the shenanigans of the Amiga project, their takeover by Commodore, and all the funny money stuff that went on.  
  
We didn’t part amicably, but Carl and I were caught up in something bigger than either of us on the money front. Along the way he was smashed into compliance while we (my WSM Group) enjoyed a brief but lucrative contract from Commodore. Once the dust settled, we were all dispatched to elsewhere.   
  
A lawsuit ensued as a result of the truncated contract, dragging out for another year. By the time I was deposed, Amiga had lost all of their engineers, and the lawyers could not understand anything I was saying about the technology. We ended up getting a settlement for 50 cents on the dollar, the day before Arbitration. The total contract was around $600K, back in 1985(?). We actually got about half of that overall.  
  
The Amiga started out in 1983(?) as a hyper-Apple II computer. But along the way, and after much money fraud, they changed their desires (per Carl) to become a “Personal Unix Machine”. That would have been a marketing disaster. By the end days, under Commodore's harsh insistence, it was finally becoming a decent consumer machine.  
  
Carl did have some interesting ideas on low-level API’s in the Amiga - forced by extreme memory limitations and (probably) the need to interface with widely disparate developers of the higher level code.   
  
But we initially came together because of Forth. I guess he never quite gave up on that. I have glanced at Rebol, but I think it is misguided. I’d rather stick with Lisp.   
  
Lisp is what Forth always wanted to become when it grew up…

## Actors
Just last week, after nearly 3 years thinking hard about the problem, I finally invented UNW-PROT for Actors, as well as OPEN-FILE (an Actor’s equiv of WITH-OPEN-FILE).

Actors don’t nest. The dynamic scope of an Actor is one FUNCALL deep from the Dispatch routine. So UNWIND-PROTECT doesn’t work for Actors.  But UNW-PROT is an Actors-equivalent to UNWIND-PROTECT.

I find the whole topic of Transactional Actors programming fascinating. I’m still exploring the limits of this style of programming. Already we can prove that it transcends Lambda Calculus, using an example that is just a few lines of code.

If you had an Actors machine architecture, there would be no program counter. Instructions would be read from a global FIFO event queue. There would be no need to segregate OS Kernel memory from user space memory. There would be no store operations. It would be a memory-safe architecture from the get-go. No need for processes and threads. You would have instruction level concurrency. No need of MMU and all the silicon real-estate devoted to managing process memory. An interrupt mechanism would simply deposit the data into a message and place that into the instruction event queue.

But lacking an Actors Machine, and forced to live on a Von Neumann architecture, I think the blend of Functionally Pure Lisp code along with Actors is probably the best of both worlds. You have the speed of today’s Call/Return programming, and the task independence (no threads, no locks) of Actors dispatching for macro tasks, and maximum concurrency. And on a multi-thread multi-Core system, maximum parallelism without even lifting a finger.

Transactional behavior is key. Either you succeed, and all your SENDS and BECOME are committed, or else it becomes as though the message were never delivered.

[Lisp Actors](https://github.com/dbmcclain/Lisp-Actors)
## See Also
### Blogs
[blog](https://guitarvydas.github.io/)

[obsidian blogs](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx-)
### Videos
[videos - programming simplicity playlist](https://www.youtube.com/@programmingsimplicity2980)
### Books
leanpub'ed (disclaimer: leanpub encourages publishing books before they are finalized - these books are WIPs)
[Programming Simplicity Takeaways, and, Programming Simplicity Broad Brush](https://leanpub.com/u/paul-tarvydas)
### Discord
[Programming Simplicity](https://discord.gg/Jjx62ypR) all welcome, I invite more discussion of these topics, esp. regarding Drawware and 0D
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
