# Markdown

Along with Markdown input, DITA-OT now provides three new transformation types to convert DITA content to Markdown, including the original syntax, GitHub-Flavored Markdown, and GitBook.

The new output formats can be used to feed DITA content into Markdown-based publishing systems or other workflows that lack the ability to process DITA XML.

## Generating Markdown output

Markdown output can be generated by passing one of the following transformation types to the dita command with the --format option:

-   To publish Markdown DITA files, use the markdown transtype.

-   To generate [GitHub-Flavored Markdown](https://github.github.com/gfm/) files, use the markdown\_github transtype.

-   To publish GitHub-Flavored Markdown and generate a SUMMARY.md table of contents file for publication via [GitBook](https://www.gitbook.com) or [mdBook](https://rust-lang.github.io/mdBook/), use the markdown\_gitbook transtype.


Run the dita command and set the value of the output --format option to the desired format, for example:

```
dita --input=input-file --format=markdown
```

where:

-   input-file is the DITA map or DITA file that you want to process.

**Related information**  


[Markdown support inside-out](https://www.oxygenxml.com/events/2017/dita-ot_day.html#Markdown_support_inside-out)

[Markdown plugin](https://www.oxygenxml.com/events/2015/dita-ot_day.html#Markdown_plugin)

[Common parameters](../parameters/parameters-base.md)

