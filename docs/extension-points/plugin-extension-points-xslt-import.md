# XSLT-import extension points

You can use these extension points to override XSLT processing steps in pre-processing and certain transformation types. The value of the `@file` attribute in the `feature` element specifies a relative path to an XSL file in the current plug-in. The plug-in installer adds a XSL import statement to the default DITA-OT code, so that the XSL override becomes part of the normal build.

## Pre-processing

You can use the following extension points to add XSLT processing to modules in the pre-processing pipeline:

-   **dita.xsl.conref**

    Overrides the pre-processing step that resolves conref.

-   **dita.xsl.maplink**

    Overrides the `maplink` step in the pre-processing pipeline. This is the step that generates map-based links.

-   **dita.xsl.mappull**

    Overrides the `mappull` step in the pre-processing pipeline. This is the step that updates navigation titles in maps and causes attributes to cascade.

-   **dita.xsl.mapref**

    Overrides the `mapref` step in the pre-processing pipeline. This is the step that resolves references to other maps.

-   **dita.xsl.topicpull**

    Overrides the `topicpull` step in the pre-processing pipeline. This is the step that pulls text into `xref` elements, as well as performing other tasks.


## Transformations

You can use the following extension points to add XSLT processing to modules in DITA-OT transformations:

-   **dita.map.eclipse.index.pre**

    Runs an Ant target before the Eclipse index extraction process.

-   **dita.xsl.eclipse.plugin**

    Overrides the default XSLT step that generates the plugin.xml file for Eclipse Help.

-   **dita.xsl.eclipse.toc**

    Overrides the default XSLT step that generates the Eclipse Help table of contents \(TOC\).

-   **dita.xsl.html.cover**

    Overrides the default HTML cover page generation process.

-   **dita.xsl.htmltoc**

    Overrides the default XSLT step that generates the HTML table of contents \(TOC\).

-   **dita.xsl.html5**

    Overrides the default HTML5 transformation. The referenced file is integrated directly into the XSLT step that generates HTML5.

-   **dita.xsl.html5.cover**

    Overrides the default HTML5 cover page generation process.

-   **dita.xsl.html5.toc**

    Overrides the default XSLT step that generates the HTML5 table of contents \(TOC\).

-   **dita.xsl.htmlhelp.map2hhc**

    Overrides the default XSLT step that generates the HTML Help contents \(.hhc\) file.

-   **dita.xsl.htmlhelp.map2hhp**

    Overrides the default XSLT step that generates the HTML Help project \(.hhp\) file.

-   **dita.xsl.xhtml**

    Overrides the default HTML or XHTML transformation, including HTML Help and Eclipse Help. The referenced file is integrated directly into the XSLT step that generates XHTML.

-   **dita.xsl.xslfo**

    Overrides the default PDF transformation. The referenced XSL file is integrated directly into the XSLT step that generates the XSL-FO.


## Example

The following two files represent a complete \(albeit simple\) plug-in that adds a company banner to the XHTML output. The plugin.xml file declares an XSLT file that extends the XHTML processing; the xsl/header.xsl file overrides the default header processing to provide a company banner.

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

