# MDITA syntax

In 2017, the Markdown plug-in was superseded by the *LwDITA* plug-in, which was bundled with DITA-OT 3.0, and added new formats for [Lightweight DITA](https://docs.oasis-open.org/dita/LwDITA/v1.0/cn01/LwDITA-v1.0-cn01.html). The `mdita` format implements the subset of Markdown features proposed in the latest specification drafts, but differs in some ways from the original [Markdown DITA](Markdown-DITA-syntax.md) format.

To apply the stricter LwDITA-specific processing to a Markdown topic, create a topic reference in your map and set the `@format` attribute to `mdita`:

```xml
<map>
  <topicref href="mdita-topic.md" format="mdita"/>
</map>
```

In this case, the first paragraph in the topic is treated as a short description, and tables are converted to DITA `<simpletable>` elements.

The *MDITA* format uses [CommonMark](https://commonmark.org/) as the underlying markup language. MDITA files must be UTF-8 encoded.

The MDITA parser processes topics according to the MDITA *“Extended profile”* proposed for LwDITA. The *"Core profile"* can be enabled for custom parser configurations.

The following Markdown constructs are parsed differently when the `@format` attribute is set to `mdita`.

## Titles and document structure

The first heading level generates a topic and the second heading level a section:

```markdown
# Topic title

## Section title
```

```xml
<topic id="topic_title">
  <title>Topic title</title>
  <body>
    <section>
      <title>Section title</title>
    </section>
  </body>
</topic>
```

The ID is generated automatically from the title content.

## Topic content

The first paragraph is treated as a `<shortdesc>` element.

```markdown
# Topic title

First paragraph.

Second paragraph.
```

```xml
<topic id="topic_title">
  <title>Topic title</title>
  <shortdesc>First paragraph.</shortdesc>
  <body>
    <p>Second paragraph.</p>
  </body>
</topic>
```

## Tables

Tables use the [MultiMarkdown](https://fletcherpenney.net/multimarkdown/) table extension format:

```markdown
| First Header | Second Header | Third Header |
| ------------ | :-----------: | -----------: |
| Content      |    _Cell_     |         Cell |
| Content      |   **Cell**    |         Cell |
```

Tables in MDITA files are converted to DITA `<simpletable>` elements:

```xml
<simpletable>
  <sthead>
    <stentry>
      <p>First Header</p></stentry>
    <stentry>
      <p>Second Header</p></stentry>
    <stentry>
      <p>Third Header</p></stentry>
  </sthead>
  <strow>
    <stentry>
      <p>Content</p></stentry>
    <stentry>
      <p><i>Cell</i></p></stentry>
    <stentry>
      <p>Cell</p></stentry>
  </strow>
  <strow>
    <stentry>
      <p>Content</p></stentry>
    <stentry>
      <p><b>Cell</b></p></stentry>
    <stentry>
      <p>Cell</p></stentry>
  </strow>
</simpletable>
```

> **Note** Cell alignment information is not preserved, as the `@align` attribute is are not available for `<simpletable>` elements.

Table cells may only contain inline content.

## MDITA map syntax

DITA maps can be written in MDITA using standard Markdown syntax for links and lists.

> **Note:** Requires DITA-OT 4.1 or newer.

In MDITA, maps use the file name extension `mditamap` to define the file as a map:

```markdown
# Map title

- [Topic title](topic.md)
  - [Nested title](nested.md)
```

```xml
<map>
  <title>Map Title</title>
  <topicref href="topic.dita" navtitle="Topic title">
    <topicref href="nested.dita" navtitle="Nested title"/>
  </topicref>
</map>
```

In MDITA, both ordered and unordered list items create `<topicref>` elements.

## Common syntax

The following common Markdown constructs are processed in the same way for both `mdita` and `markdown` topics.

### Hard line breaks

A line break that is preceded by two or more spaces is parsed as a hard line break. Because DITA doesn’t have a `<br>` element for line break, hard line breaks are converted into `<?linebreak?>` processing instructions.

```markdown
foo··
baz
```

```xml
<p>foo<?linebreak?>baz</p>
```

The LwDITA plug-in contains extensions for HTML5 and PDF outputs to generate line breaks.

### Links

The format of local link targets is detected based on file name extension. The following extensions are treated as DITA files:

|extension|format|
|---------|------|
|`.dita`|`dita`|
|`.xml`|`dita`|
|`.md`|`markdown`|
|`.markdown`|`markdown`|

All other link targets detect the `format` from the file name extension and are treated as non-DITA files. Absolute link targets are treated as external scope links:

```markdown
[Markdown](test.md)
[DITA](test.dita)
[HTML](test.html)
[External](http://www.example.com/test.html)
```

```xml
<xref href="test.md">Markdown</xref>
<xref href="test.dita">DITA</xref>
<xref href="test.html" format="html">HTML</xref>
<xref href="http://www.example.com/test.html" format="html" scope="external">External</xref>
```

### Images

Images used in inline content are processed with inline placement. If a block-level image contains a title, it is treated as an image wrapped in a figure element:

```markdown
An inline ![Alt](test.jpg).

![Alt](test.jpg)

![Alt](test.jpg 'Title')
```

```xml
<p>An inline <image href="test.jpg"><alt>Alt</alt></image>.</p>
<image href="test.jpg" placement="break">
  <alt>Alt</alt>
</image>
<fig>
  <title>Title</title>
  <image href="test.jpg">
    <alt>Alt</alt>
  </image>
</fig>
```

### Key references

Keys can be referenced using standard Markdown syntax for [shortcut reference links](https://spec.commonmark.org/0.30/#shortcut-reference-link):

```markdown
[key]
[link text][key]
![image-key]
```

```xml
<xref keyref="key"/>
<xref keyref="key">link text</xref>
<image keyref="image-key"/>
```

### Inline

The following inline elements are supported:

```markdown
**bold**
_italic_
`code`
~~strikethrough~~
```

```xml
<b>bold</b>
<i>italic</i>
<codeph>code</codeph>
<ph status="deleted">strikethrough</ph>
```

### Lists

Standard Markdown syntax is used for both ordered \(numbered\) and unordered \(bulleted\) lists.

Unordered list items can be marked up using either asterisks “`*`” or hyphens “`-`” as list markers:

```markdown
* one
* two
  - three
  - four
```

```xml
<ul>
  <li>one</li>
  <li>two
    <ul>
      <li>three</li>
      <li>four</li>
    </ul>
  </li>
</ul>
```

Ordered lists use either numbers or number signs “`#`”, followed by a period:

```markdown
1.  one
2.  two
    #. three
    #. four
```

```xml
<ol>
  <li>one</li>
  <li>two
    <ol>
      <li>three</li>
      <li>four</li>
    </ol>
  </li>
</ol>
```

> **Note:** Markdown DITA supports both loose and [tight](https://spec.commonmark.org/0.30/#tight) list spacing \(with no blank lines between list items\). MDITA treats all lists as [loose](https://spec.commonmark.org/0.30/#loose), and wraps each list item in a paragraph \(`<li><p>item</p></li>`\).

Definition lists use the [PHP Markdown Extra](https://michelf.com/projects/php-markdown/extra/#def-list) format with a single-line term followed by a colon and the definition:

```markdown
Term
: Definition.
```

```xml
<dl>
  <dlentry>
    <dt>Term</dt>
    <dd>Defintion.</dd>
  </dlentry>
</dl>
```

Each definition list entry must have only one term and contain only inline content.

### Metadata

A [YAML](https://www.yaml.org/) metadata block as defined in the [pandoc\_metadata\_block](https://pandoc.org/MANUAL.html#extension-yaml_metadata_block) extension can be used to specify metadata elements for the DITA prolog.

The supported elements are:

-   `author`
-   `source`
-   `publisher`
-   `permissions`
-   `audience`
-   `category`
-   `keyword`
-   `resourceid`

Any unrecognized keys are output using the `<data>` element.

```markdown
---
author:
  - Author One
  - Author Two
source: Source
publisher: Publisher
permissions: Permissions
audience: Audience
category: Category
keyword:
  - Keyword1
  - Keyword2
resourceid:
  - Resourceid1
  - Resourceid2
workflow: review
---

# Sample with YAML header
```

```xml
<title>Sample with YAML header</title>
<prolog>
  <author>Author One</author>
  <author>Author Two</author>
  <source>Source</source>
  <publisher>Publisher</publisher>
  <permissions view="Permissions"/>
  <metadata>
    <audience audience="Audience"/>
    <category>Category</category>
    <keywords>
      <keyword>Keyword1</keyword>
      <keyword>Keyword2</keyword>
    </keywords>
  </metadata>
  <resourceid appid="Resourceid1"/>
  <resourceid appid="Resourceid2"/>
  <data name="workflow" value="review"/>
</prolog>
```

