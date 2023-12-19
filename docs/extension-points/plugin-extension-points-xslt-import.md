# XSLT-import extension points

You can use these extension points to override XSLT processing steps in pre-processing and certain transformation types. The value of the `@file` attribute in the `<feature>` element specifies a relative path to an XSL file in the current plug-in. The plug-in installer adds a XSL import statement to the default DITA-OT code, so that the XSL override becomes part of the normal build.

## Pre-processing

You can use the following extension points to add XSLT processing to modules in the pre-processing pipeline:

-   **__dita.xsl.conref__**

    Overrides the pre-processing step that resolves conref.

-   **__dita.xsl.maplink__**

    Overrides the `maplink` step in the pre-processing pipeline. This is the step that generates map-based links.

-   **__dita.xsl.mappull__**

    Overrides the `mappull` step in the pre-processing pipeline. This is the step that updates navigation titles in maps and causes attributes to cascade.

-   **__dita.xsl.mapref__**

    Overrides the `mapref` step in the pre-processing pipeline. This is the step that resolves references to other maps.

-   **__dita.xsl.topicpull__**

    Overrides the `topicpull` step in the pre-processing pipeline. This is the step that pulls text into `<xref>` elements, as well as performing other tasks.


## Transformations

You can use the following extension points to add XSLT processing to modules in DITA-OT transformations:

-   **__dita.map.eclipse.index.pre__**

    Runs an Ant target before the Eclipse index extraction process.

-   **__dita.xsl.eclipse.plugin__**

    Overrides the default XSLT step that generates the `plugin.xml` file for Eclipse Help.

-   **__dita.xsl.eclipse.toc__**

    Overrides the default XSLT step that generates the Eclipse Help table of contents \(TOC\).

-   **__dita.xsl.html.cover__**

    Overrides the default HTML cover page generation process.

-   **__dita.xsl.htmltoc__**

    Overrides the default XSLT step that generates the HTML table of contents \(TOC\).

-   **__dita.xsl.html5__**

    Overrides the default HTML5 transformation. The referenced file is integrated directly into the XSLT step that generates HTML5.

-   **__dita.xsl.html5.cover__**

    Overrides the default HTML5 cover page generation process.

-   **__dita.xsl.html5.toc__**

    Overrides the default XSLT step that generates the HTML5 table of contents \(TOC\).

-   **__dita.xsl.htmlhelp.map2hhc__**

    Overrides the default XSLT step that generates the HTML Help contents \(`.hhc`\) file.

-   **__dita.xsl.htmlhelp.map2hhp__**

    Overrides the default XSLT step that generates the HTML Help project \(`.hhp`\) file.

-   **__dita.xsl.xhtml__**

    Overrides the default HTML or XHTML transformation, including HTML Help and Eclipse Help. The referenced file is integrated directly into the XSLT step that generates XHTML.

-   **__dita.xsl.xslfo__**

    Overrides the default PDF transformation. The referenced XSL file is integrated directly into the XSLT step that generates the XSL-FO.


## Example

The following two files represent a complete \(albeit simple\) plug-in that adds a company banner to the XHTML output. The `plugin.xml` file declares an XSLT file that extends the XHTML processing; the `xsl/header.xsl` file overrides the default header processing to provide a company banner.

```
<?xml version="1.0" encoding="UTF-8"?>
<plugin id="com.example.brandheader">
  <feature extension="dita.xsl.xhtml" file="xsl/header.xsl"/>
</plugin>
```

```
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:template name="gen-user-header">
    <div>
      <img src="http://www.example.com/company_banner.jpg" 
           alt="Example Company Banner"/>
    </div>
  </xsl:template>
</xsl:stylesheet>
```

