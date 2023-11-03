# The Advantages of Using Draw.io for Odin0D

Draw.io offers several key benefits for editing and visualizing diagrams in the context of Odin0D, making it a suitable choice for this purpose:

## Editor-Friendly Approach
Draw.io provides an intuitive and user-friendly interface for diagram editing, ensuring that editors can easily manipulate and design diagrams without the need for complex compiler code integration.

## Flexible Editor Choice
Odin0D allows users to work with any text editor that can save diagrams in an accessible format. Draw.io supports various export options, including SVG, XML, and graphml, making it compatible with a wide range of editors.

## Dumbed-Down SVG
Dumbed-down SVG export simplifies the diagram representation by disregarding over-complicated SVG features. This approach aligns with the concept of "rules" similar to using English in textual programming languages.

When you simply ignore unneeded features of SVG, you are left with:
- rect
- ellipse
- line, arrow
- text
- grouping

You don't need to modify SVG, just ignore the bits that are outside of the scope of the *programming language*.

I found that using PROLOG syntax made it easier to grok the bits of SVG that are interesting.  YMMV.  If I had time, I would look at miniKanren, too.

Currently, I used OhmJS to parse (grok) SVG and attempts to use diagrams as legal programs.  Once parsed, by the OhmJS engine, I used *semantic rules* written in `.rwr` format (emits JavaScript that is compatible with OhmJS) to exhale code in the language of my choice, e.g. Python, JavaScript, Odin, etc.

## Text Formats for Easy Parsing
Odin0D encourages using text formats such as XML, which are easily parsed with existing technology. This approach simplifies the process of working with diagrams and facilitates compatibility with various tools.

Utilizing tools like PEG (Parsing Expression Grammar), including alternatives such as OhmJS, can further enhance the parsing capabilities.

## Alternative Diagramming Tools
While Draw.io is a suitable choice, users can also explore alternative diagramming tools such as yEd and Excalidraw to cater to their specific needs and preferences.

## Conclusion
By using Draw.io in Odin0D, editors and users can benefit from a straightforward and versatile approach to diagram creation and editing while ensuring compatibility with a variety of text editors and tools.


# Appendix - ChatGPT Prompt
summarize the following markdown as a subsection for a chapter in a book
# Appendix - Point-Form Notes

- let editor edit
    - don't complicate the editor by inserting compiler code
- choose any editor that saves diagram in an accessible form
    - dumbed-down SVG
        - simply ignore over-complicated uses of SVG
        - Arrowgrams
            - export diagram as SVG
                - draw.io allows exporting as SVG
            - "rules" for what will be parsed
                - akin to "rules" for using English in textual programming languages
        - rect
        - ellipse
        - line, arrow
        - text
        - grouping
    - XML, graphml, etc.
        - text format (e.g. XML) - easily parsed with existing tech
            - PE
                - OhmJS is "better" PEG
        - yEd
        - draw.io
        - Excalidraw

# Appendix - See Also

## See Also

### References

https://guitarvydas.github.io/2021/12/15/References.html

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
