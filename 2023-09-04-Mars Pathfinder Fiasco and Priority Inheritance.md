
One of the early unmanned missions to Mars was a robot called the Mars Pathfinder.

It got all of the way to Mars, but started continuously rebooting when it landed.

This created several questions:
1. Why was it rebooting?
2. How could the Pathfinder software be updated remotely?

The first question involved sub-questions like "how did the rigorous pre-flight testing not catch the problem?", etc.

The second question was a practical one.  The Pathfinder was on the surface of Mars, a long, long distance away from Earth and the engineering team.  The only way to update the software was to send an update by radio.  Radio worked only on a line-of-sight basis. Pathfinder could not receive radio transmissions if it was facing away from the part of Earth that was sending the radio signals. That meant that the software update could only happen when the correct part of Earth was facing the correct part of Mars.  If either planet's revolution turned it to face the wrong way, then the radio transmission could not be received.   What were the time windows that would work?  How long were the time windows?  Was the update small enough to be sent as a radio transmission during one time window, or, would the update need to be sent in chunks during successive time windows?

In the end, both problems were solved and the Pathfinder stopped rebooting and could carry out its mission.  This failure was rebranded as an Engineering Success.

In my opinion, though, this episode shows some very deep flaws in how we construct software, like
- software is compiled into big blobs of tightly coupled binary - updating a single line of code required recompiling the whole blob and sending the whole blob, instead of sending only a few bytes
- religious belief in the efficacy of using synchronous programming languages, i.e. software languages that are function-based (FP, FORTRAN, Python, Rust, Lisp, etc., etc.)

- ad-hoc testing of the methods and ad-hoc fixing of the methods, both, of which are claimed to be unnecessary using formal methods (wrong)
- whack-a-mole



# Appendix - See Also

### References

[https://guitarvydas.github.io/2004/01/06/References.html](https://guitarvydas.github.io/2024/01/06/References.html)

### Blog
[blog](https://guitarvydas.github.io/)

### Blog
[obsidian blogs](https://publish.obsidian.md/programmingsimplicity) (see blogs that begin with a date 202x-xx-xx-)
### Videos
[videos - programming simplicity playlist](https://www.youtube.com/@programmingsimplicity2980)
### Books (WIP)
[leanpub](https://leanpub.com/u/paul-tarvydas)
### Pamphlets
[gumroad](https://tarvydas.gumroad.com/l/dvtej?_gl=1*o7hy6z*_ga*MjA0NzUyMDY1Mi4xNzA3NDc3MDIx*_ga_6LJN6D94N6*MTcwNzQ3NzAyMC4xLjEuMTcwNzQ3NzI5Ni4wLjAuMA..)
### Discord
[Programming Simplicity](https://discord.gg/Jjx62ypR) all welcome, I invite more discussion of these topics, esp. regarding Drawware and 0D
### Twitter
@paul_tarvydas

<script src="https://utteranc.es/client.js" 
        repo="guitarvydas/guitarvydas.github.io" 
        issue-term="pathname" 
        theme="github-light" 
        crossorigin="anonymous" 
        async> 
</script> 
