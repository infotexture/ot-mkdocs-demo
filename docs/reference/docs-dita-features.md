# DITA features in the documentation

DITA Open Toolkit uses various recent DITA features in the project documentation.

The [source files](https://github.com/dita-ot/docs) for the DITA-OT documentation include examples of the following DITA features \(among others\):

-   subjectScheme classification for controlling available attributes
-   profiling and branch filtering \(novice/expert content\)
-   extending topics with conref push
-   keys and key references
-   XML mention domain

## Subject schemes

Various topics, sections and elements in the docs are profiled by audience:

```
<li id="novice-variables-last" audience="novice">
  <p id="common-format-info">
    <varname>format</varname> is the output format (transformation type). This argument corresponds to the
    common parameter <xref keyref="parameters-base/transtype"/>. Use the same values as for the
      <parmname>transtype</parmname> build parameter, for example <option>html5</option> or
      <option>pdf</option>.</p>
</li>
```

An “audience” subject scheme controls the values that are available for the `@audience` attribute:

```
<subjectdef keys="audience">
  <subjectdef keys="novice"/>
  <subjectdef keys="expert"/>
  <subjectdef keys="xslt-customizer"/>
</subjectdef>
```

A dedicated subject scheme map defines several series of permissible values for `@outputclass` attributes, which apply styling to elements on the project website, enable [extended codeblock processing](extended-functionality.md) such as whitespace visualization and line numbering in PDF output, or trigger [HTML5-compliant syntax highlighting](https://www.w3.org/TR/html52/textlevel-semantics.html#the-code-element) via [prism.js](https://prismjs.com).

```
<schemeref href="subjectscheme-outputclass.ditamap"/>
```

## Branch filtering: re-using profiled content

**Installing DITA-OT** pulls a subset of the build description from **using the dita command**, filtered to display only content deemed suitable for novice users under [Building output](../topics/first-build-using-dita-command.md):

```
<topicref href="using-dita-command.dita"
          keys="first-build-using-dita-command" locktitle="yes">
  <topicmeta>
    <navtitle>Building output</navtitle>
  </topicmeta>
  <ditavalref href="../resources/novice.ditaval">
    <ditavalmeta>
      <dvrResourcePrefix>first-build-</dvrResourcePrefix>
    </ditavalmeta>
  </ditavalref>
</topicref>
```

The same content appears later in [Using the dita command](../topics/build-using-dita-command.md) with additional information on arguments, options and examples.

```
<topicref href="using-dita-command.dita"
          keys="build-using-dita-command" locktitle="yes">
  <topicmeta>
    <navtitle>Using the <cmdname>dita</cmdname> command</navtitle>
  </topicmeta>
  <ditavalref href="../resources/expert.ditaval">
    <ditavalmeta>
      <dvrResourcePrefix>build-</dvrResourcePrefix>
    </ditavalmeta>
  </ditavalref>
```

## Conref push

The docs build uses the conref push mechanism \(with the `pushreplace`, `mark`, and `pushafter` [conactions](http://docs.oasis-open.org/dita/dita/v1.3/errata01/os/complete/part1-base/langRef/attributes/theconactionattribute.html)\) to extend the parameter descriptions embedded in the default plug-ins:

```
<plentry id="args.csspath">
  <pt>
    <parmname>args.csspath</parmname>
  </pt>
  <pd conaction="pushreplace" conref="parameters-html5.dita#html5/args.csspath.desc">
    <div conref="./ant-parameters-details.dita#base-html/args.csspath.desc"/>
  </pd>
  <pd conaction="mark" conref="parameters-html5.dita#html5/args.csspath.desc"/>
  <pd conaction="pushafter">
    <div conref="./ant-parameters-details.dita#base-html/args.csspath.details"/>
  </pd>
</plentry>
```

The pushed content appears in the output after the default description. \(See [HTML-based output parameters](../parameters/parameters-base-html.md).\)

**Tip:** You could also use the same mechanism to extend the documentation with custom information that applies only to your company’s toolkit distribution.

## Keys and key references

The `key-definitions.ditamap` defines keys for version references, re-usable links, etc.

This key definition defines the maintenance release version:

```
<keydef keys="maintenance-version">
  <topicmeta>
    <keywords>
      <keyword>4.0.2</keyword>
    </keywords>
  </topicmeta>
</keydef>
```

In topics, the keyword is used in place of hard-coded version references:

```language-xml
<title>DITA Open Toolkit <keyword keyref="maintenance-version"/> Release Notes</title>
```

## XML mention domain

The docs use the [XML mention domain](http://docs.oasis-open.org/dita/dita/v1.3/os/part3-all-inclusive/langRef/containers/xml-mention-domain.html#xml-mention-domain) to mark up XML elements and attributes:

```language-xml
<li id="1777">
  DITA 1.3: Initial support has been added for the <xmlatt>orient</xmlatt>
  attribute on <xmlelement>table</xmlelement> elements. These changes allow
  Antenna House Formatter to render tables in landscape mode when the
  <xmlatt>orient</xmlatt> attribute is set to <option>land</option>. […]
</li>
```

When the toolkit generates output for the sample above:

-   the XML element name is wrapped in angle brackets as `table`
-   the attribute name is prefixed with an “at” sign as `@orient`

