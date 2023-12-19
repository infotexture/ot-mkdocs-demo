# Markdown DITA syntax

In 2015, the original *DITA-OT Markdown* plug-in introduced a series of conventions to convert [Markdown](https://daringfireball.net/projects/markdown/) content to DITA, and vice-versa. This Markdown flavor was called *“Markdown DITA”*. The `markdown` format adds several complementary constructs to represent DITA content in Markdown, beyond those proposed for the [MDITA](MDITA-syntax.md) format in the [Lightweight DITA](https://docs.oasis-open.org/dita/LwDITA/v1.0/cn01/LwDITA-v1.0-cn01.html) specification drafts.

To add a Markdown topic to a DITA publication, create a topic reference in your map and set the `@format` attribute to `markdown`. This allows the toolkit to recognize the source file as Markdown and convert it to DITA:

```xml
<map>
  <topicref href="markdown-dita-topic.md" format="markdown"/>
</map>
```

In this case, the first paragraph in the topic is treated as a body paragraph, and each heading level generates a nested topic.

The *Markdown DITA* format uses [CommonMark](https://commonmark.org/) as the underlying markup language, with several extensions as noted below. Markdown DITA files must be UTF-8 encoded.

The following Markdown constructs are parsed differently when the `@format` attribute is set to `markdown`.

## Titles and document structure

Each heading level generates a topic and associated title:

```markdown
# Topic title

## Nested topic title
```

```xml
<topic id="topic_title">
  <title>Topic title</title>
  <topic id="nested_topic_title">
    <title>Nested topic title</title>
  </topic>
</topic>
```

Pandoc [header attributes](https://pandoc.org/MANUAL.html#extension-header_attributes) or PHP Markdown Extra [special attributes](https://michelf.ca/projects/php-markdown/extra/#spe-attr) can be used to define `id` or `outputclass` attributes:

```markdown
# Topic title {#carrot .juice audience=novice}
```

```xml
<topic id="carrot" outputclass="juice" audience="novice">
  <title>Topic title</title>
```

If topic ID is not defined using header attributes, the ID is generated from title contents.

If the Markdown document doesn’t contain a level 1 heading, one is generated based on YAML metadata or from the document file name.

## Topic content

In Markdown DITA documents, all paragraphs appear inside the `body` element.

```markdown
# Topic title

First paragraph.

Second paragraph.
```

```xml
<topic id="topic_title">
  <title>Topic title</title>
  <body>
    <p>First paragraph.</p>
    <p>Second paragraph.</p>
  </body>
</topic>
```

## Specialization types

The following class values in [header attributes](https://pandoc.org/MANUAL.html#extension-header_attributes) have a special meaning on level 1 headings:

-   `concept`
-   `task`
-   `reference`

They can be used to change the Markdown DITA topic type to one of the built-in structural specialization types.

```markdown
# Task {.task}

Context

1.  Command

    Info.
```

```xml
<task id="task">
  <title>Task </title>
  <taskbody>
    <context>
      <p>Context</p>
    </context>
    <steps>
      <step>
        <cmd>Command</cmd>
        <info>
          <p>Info.</p>
        </info>
      </step>
    </steps>
  </taskbody>
</task>
```

The other way to use specialization types is by defining a [schema](Markdown-schemas.md) for the document.

## Sections

The following class values in [header attributes](https://pandoc.org/MANUAL.html#extension-header_attributes) have a special meaning on heading levels other than 1:

-   `section`
-   `example`

They are used to generate [`section`](https://docs.oasis-open.org/dita/v1.2/os/spec/langref/section.html) and [`example`](https://docs.oasis-open.org/dita/v1.2/os/spec/langref/example.html) elements:

```markdown
# Topic title

## Section title {.section}

## Example title {.example}
```

```xml
<topic id="topic_title">
  <title>Topic title</title>
  <body>
    <section>
      <title>Section title</title>
    </section>
    <example>
      <title>Example title</title>
    </example>
  </body>
</topic>
```

## Tables

Tables use the [MultiMarkdown](https://fletcherpenney.net/multimarkdown/) table extension format:

```markdown
| First Header | Second Header | Third Header |
| ------------ | :-----------: | -----------: |
| Content      |          _Long Cell_        ||
| Content      |   **Cell**    |         Cell |
```

Tables in Markdown DITA files are converted to the [OASIS exchange table model](https://www.oasis-open.org/specs/tm9901.html):

```xml
<table>
  <tgroup cols="3">
    <colspec colname="col1" colnum="1"/>
    <colspec colname="col2" colnum="2"/>
    <colspec colname="col3" colnum="3"/>
    <thead>
      <row>
        <entry colname="col1">First Header</entry>
        <entry align="center" colname="col2">Second Header</entry>
        <entry align="right" colname="col3">Third Header</entry>
      </row>
    </thead>
    <tbody>
      <row>
        <entry colname="col1">Content</entry>
        <entry align="center" namest="col2" nameend="col3" colname="col2"><i>Long Cell</i></entry>
      </row>
      <row>
        <entry colname="col1">Content</entry>
        <entry align="center" colname="col2"><b>Cell</b></entry>
        <entry align="right" colname="col3">Cell</entry>
      </row>
    </tbody>
  </tgroup>
</table>
```

Table cells may only contain inline content and column spans; block content and row spans are not supported in Markdown DITA.

## Notes

Notes can be written using the syntax defined in the Material for MkDocs [admonition extension](https://squidfunk.github.io/mkdocs-material/reference/admonitions/).

> **Note:** Requires DITA-OT 4.1 or newer.

```markdown
!!! note

    Note content.
```

```xml
<note>
  <p>Note Content.</p>
</note>
```

Different note types can be defined by changing the type qualifier keyword.

```markdown
!!! info

    Info content.
```

```xml
<note type="info">
  <p>Info Content.</p>
</note>
```

## Markdown DITA map syntax

DITA maps can be written in Markdown using standard Markdown syntax for links and lists.

> **Note:** Requires DITA-OT 4.1 or newer.

In Markdown DITA, maps use the [schema](Markdown-schemas.md) key in the YAML front matter block to define the file as a map:

```markdown
---
$schema: urn:oasis:names:tc:dita:xsd:map.xsd
---

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

Unordered list items create `<topicref>` elements, and ordered list items create `<topicref>` elements with `collection-type="sequence"`.

## Key definitions

Keys can be defined using standard Markdown syntax for [link reference definitions](https://spec.commonmark.org/0.30/#link-reference-definition).

```markdown
---
$schema: urn:oasis:names:tc:dita:xsd:map.xsd
---

[key-name]: topic.md
```

```xml
<map>
  <keydef href="topic.dita" navtitle="Topic title"/>
</map>
```

## Relationship tables

Relationship tables are tables with links inside cells.

```markdown
---
$schema: urn:oasis:names:tc:dita:xsd:map.xsd
---

| [Help](topic.md)  |                           |
| ----------------- | ------------------------- |
| [Topic](topic.md) | [Reference](reference.md) |
```

```xml
<map>
  <reltable>
    <relheader>
      <relcolspec>
        <topicref href="help.dita"/>
      </relcolspec>
      <relcolspec/>
    </relheader>
    <relrow>
      <relcell>
        <topicref href="topic.dita"/>
      </relcell>
      <relcell>
        <topicref href="reference.dita"/>
      </relcell>
    </relrow>
  </reltable>
</map>
```

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

