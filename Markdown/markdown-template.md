# Markdown template

<Add overview/description here>

The below line will generate a table of contents for levels 1 and 2 at a level 2
`[TOC levels=2]: # "## Table of contents"`

[TOC levels=2]: # "## Table of contents"

## Table of contents
- [Font types/formatting](#font-typesformatting)
- [Collapsible markdown](#collapsible-markdown)
- [Hint/Info/Alerts](#hintinfoalerts)
- [Table](#table)

Bullet list of items
* item 1
* item 2

Numbered list of items
1. item 1
2. item 2

Checklist items
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

## Collapsible markdown

***WARNING***: The below collapsible sections may not display correctly in PyCharm Viewer, but they do work on github

A collapsible section containing markdown.  Note that this does not display correctly with Markdown Enhanced previewer
in PyCharm.  A black line is needed after the summary closing tag.  A blank line is needed after the closing details tag as well.

<details>
<summary>Click to expand!</summary>

### Collapsible Section with Markdown

1. The heading above this numbered list as well as the numbered list will be hidden.
2. Second Item
   3. Sub item
   4. Sub Item
</details>

The below is a collapsible section with a code block in it


<details>
<summary>Summary - Collapsed Markdown Block</summary>
<p>

```c#
public class Order
{
    public int OrderId { get; set; }
    public int CustomerId { get; set; }

    public List<int> Products { get; set; }
}
```

</p>
</details>

## Hint/Info/Alerts

:bulb: **Hint:** An example for capturing a hint or important idea

> **Warning**: A quoted/indented warning block with Warning bolded.

> :warning: Warning in block quote format using the `:warning:` icon

| **Warning**: Warning note done as a table |
|:------------------------------------------|

## Table

| Column1                                  | Column 2                             |
|:-----------------------------------------|:-------------------------------------|
| Row 1                                    | Row 1 Description                    |
| Row 2                                    | Row 2 Description                    |
| Row using a reference link (e.g. github) | [Markdown Guide][Markdown Guide.org] |

### Links
* Enclose alias in brackets and URL in parenthesis right after:
  * [link text](http://dev.nodeca.com)
  * `[link text](http://dev.nodeca.com)`
* Link with title and mouse over text:
  * `[link with title](http://nodeca.github.io/pica/demo/ "title text!")`
  * [link with title](http://nodeca.github.io/pica/demo/ "title text!")
* Links using references: The first set of brackets surrounds the text that should appear linked. The second set of brackets displays a label used to point to the link you’re storing elsewhere in your document.
  * Reference link: [link text][reference]
  * * `[link text][reference]`

<!--- Comment: Add any Reference links below -->
[reference]: https://en.wikipedia.org/wiki/Hobbit#Lifestyle  "Title"
[Markdown Guide.org]: https://www.markdownguide.org/basic-syntax/
[HackMD-it]: https://hackmd.io/c/tutorials/%2Fs%2Fhackmd-it
[Markdown Icon]: https://d33wubrfki0l68.cloudfront.net/f1f475a6fda1c2c4be4cac04033db5c3293032b4/513a4/assets/images/markdown-mark-white.svg

### Images
* Image with direct URL and an alias:
  * ![Minion](https://d33wubrfki0l68.cloudfront.net/f1f475a6fda1c2c4be4cac04033db5c3293032b4/513a4/assets/images/markdown-mark-white.svg)
  * `![Minion](https://d33wubrfki0l68.cloudfront.net/f1f475a6fda1c2c4be4cac04033db5c3293032b4/513a4/assets/images/markdown-mark-white.svg)`
* Image with Alias and Mouse over text:
  * ![Stormtroopocat](https://d33wubrfki0l68.cloudfront.net/f1f475a6fda1c2c4be4cac04033db5c3293032b4/513a4/assets/images/markdown-mark-white.svg " Mouse Over Markdown Icon")
  * `![Stormtroopocat](https://d33wubrfki0l68.cloudfront.net/f1f475a6fda1c2c4be4cac04033db5c3293032b4/513a4/assets/images/markdown-mark-white.svg " Mouse Over Markdown Icon")`