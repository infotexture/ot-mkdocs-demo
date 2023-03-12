# Preview support for Lightweight DITA

DITA-OT provides preview support for the authoring formats proposed for [Lightweight DITA](http://docs.oasis-open.org/dita/LwDITA/v1.0/cn01/LwDITA-v1.0-cn01.pdf), or “LwDITA”. The XDITA, MDITA and HDITA formats are alternative representations of DITA content in XML, Markdown and HTML5.

**Attention:** Since [Lightweight DITA](http://docs.oasis-open.org/dita/LwDITA/v1.0/cn01/LwDITA-v1.0-cn01.pdf) has not yet been released as a formal specification, the implementation for XDITA, MDITA and HDITA authoring formats is subject to change. Future versions of DITA Open Toolkit will be updated as LwDITA evolves.

## XDITA

XDITA is the LwDITA authoring format that uses XML to structure information. XDITA is a subset of DITA, with new multimedia element types added to support interoperability with HTML5. XDITA is designed for users who want to write DITA content but who do not want \(or need\) the full power of DITA.

The XDITA parser included in the `org.lwdita` plug-in provides preliminary support for XDITA maps and XDITA topics.

To apply XDITA-specific processing to topics in an XDITA map or a full DITA 1.3 map, set the `@format` attribute on a `topicref` to `xdita`:

```
<map>
  <topicref href="xdita-topic.xml" **format="xdita"**/>
</map>
```

**Tip:** For examples of cross-format content sharing between topics in XDITA, HDITA, extended-profile MDITA, and DITA 1.3, see the LwDITA sample files in the DITA-OT installation directory under plugins/org.oasis-open.xdita.v0\_2\_2/samples.

## MDITA

MDITA is the LwDITA authoring format based on Markdown. It is designed for users who want to write structured content with the minimum of overhead, but who also want to take advantage of the reuse mechanisms associated with the DITA standard and the multi-channel publishing afforded by standard DITA tooling.

Recent proposals for LwDITA include two profiles for authoring MDITA topics:

-   The “Core profile” is based on [GitHub-Flavored Markdown](https://github.github.com/gfm/) and includes elements that are common to many other Markdown implementations.
-   The “Extended profile” borrows additional features from other flavors of Markdown to represent a broader range of DITA content with existing plain-text syntax conventions.

The Markdown DITA parser included in the `org.lwdita` plug-in provides preliminary support for these profiles and additional Markdown constructs as described in the syntax reference.

To apply LwDITA-specific processing to Markdown topics, set the `@format` attribute to `mdita`:

```
<map>
  <topicref href="mdita-topic.md" **format="mdita"**/>
</map>
```

In this case, the first paragraph in the topic will be treated as a short description, for example, and additional metadata can be specified for the topic via a YAML front matter block.

**Note:** Setting the `@format` attribute to `mdita` triggers stricter parsing than the more lenient document parsing approach that is applied to `markdown` documents.

**Attention:** The MDITA map format is not yet supported. To include Markdown content in publications, use an XDITA map or a DITA 1.3 map.

## HDITA

HDITA is the LwDITA authoring format based on HTML5, which is intended to support structured content authoring with tools designed for HTML authoring. HDITA also uses custom data attributes to provide interoperability with DITA.

The HDITA parser included in the `org.lwdita` plug-in provides preliminary support for these constructs.

To apply LwDITA-specific processing to HTML topics, set the `@format` attribute to `hdita`:

```
<map>
  <topicref href="hdita-topic.html" **format="hdita"**/>
</map>
```

**Attention:** The HDITA map format is not yet supported. To include HDITA content, use an XDITA map or a DITA 1.3 map.

## Converting lightweight formats to DITA XML

When you add LwDITA topics to a DITA publication, the content is temporarily converted to DITA in the background when generating other output formats like HTML or PDF, but the source files remain unchanged.

If you prefer to maintain this content in DITA in the future, you can generate DITA output by passing the --format=dita option on the command line.

This converts all input files \(both LwDITA formats and DITA XML\) to [Normalized DITA](dita2dita.md). You can then copy the generated DITA files from the output folder to your project and replace references to the lightweight topics with their DITA equivalents.

