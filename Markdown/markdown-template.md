# Markdown template

A markdown template to be used when creating a standard markdown file.

[TOC levels=2]: # "### Table of contents"

## Level 2 Topic

Bullet list of items
* item 1
* item 2

##  Checklist items

- [x] Checked task item
- [ ] Unchecked item
- [ ] Add a tag

## Font types/formatting

- **Bold**
- *Italic*
- Super^script^
- Sub~script~
- ~~Crossed~~
- ==Highlight==

## Hint/Info

:bulb: **Hint:** An example for capturing a hint or important idea

## Table

| Column1                                  | Column 2                     |
|:-----------------------------------------|:-----------------------------|
| Row 1                                    | Row 1 Description            |
| Row 2                                    | Row 2 Description            |
| Row using a reference link (e.g. github) | [:link:][Markdown Guide.org] |

[Markdown Guide.org]: https://www.markdownguide.org/basic-syntax/
[HackMD-it]: https://hackmd.io/c/tutorials/%2Fs%2Fhackmd-it


### Links
* Enclose alias in brackets and URL in parenthesis right after:
  * [link text](http://dev.nodeca.com)
  * `[link text](http://dev.nodeca.com)`
* Link with title and mouse over text:
  * `[link with title](http://nodeca.github.io/pica/demo/ "title text!")`
  * [link with title](http://nodeca.github.io/pica/demo/ "title text!")

* Links using references: The first set of brackets surrounds the text that should appear linked. The second set of brackets displays a label used to point to the link you’re storing elsewhere in your document.
  * `[link text][reference]`
  * Reference link: [link text][reference]\

<!---
Reference links below
-->
[reference]: https://en.wikipedia.org/wiki/Hobbit#Lifestyle  "Title"

### Images
* Image with direct URL and an alias:
  * `![Minion](https://octodex.github.com/images/minion.png)`
* Image with Alias and Mouse over text:
  * `![Stormtroopocat](https://octodex.github.com/images/stormtroopocat.jpg " The Stormtroopocat")`