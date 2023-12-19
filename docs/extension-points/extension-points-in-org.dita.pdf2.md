# Extension points in `org.dita.pdf2`

Certain extension points are specific to the PDF transformation \(formerly known as “PDF2”\). 

-   **__depend.org.dita.pdf2.format__**

    Formatting target

-   **__depend.org.dita.pdf2.format.post__**

    Formatting post-target

-   **__depend.org.dita.pdf2.format.pre__**

    Formatting pre-target

-   **__depend.org.dita.pdf2.index__**

    Indexing target

-   **__depend.org.dita.pdf2.init.pre__**

    Initialization pre-target

-   **__dita.conductor.pdf2.formatter.check__**

    Formatter check

-   **__dita.conductor.pdf2.param__**

    Pass parameters to the PDF transformation.

-   **__dita.xsl.xslfo__**

    Overrides the default PDF transformation. The referenced XSL file is integrated directly into the XSLT step that generates the XSL-FO.

-   **__dita.xsl.xslfo.i18n-postprocess__**

    PDF I18N postprocess import

-   **__org.dita.pdf2.catalog.relative__**

    Adds the content of a catalog file to the main catalog file for the PDF plug-in.

-   **__org.dita.pdf2.xsl.topicmerge__**

    PDF2 topic merge XSLT import


