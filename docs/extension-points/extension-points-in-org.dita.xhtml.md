# Extension points in `org.dita.xhtml`

The `org.dita.xhtml` plug-in provides shared extension points that can be used to modify processing in HTML-based transformation types such as Eclipse help, HTML Help, and XHTML. 

-   **__dita.conductor.html.param__**

    Pass parameters to the HTML and HTML Help transformations.

-   **__dita.conductor.xhtml.param__**

    Pass parameters to the XHTML and Eclipse Help transformations.

-   **__dita.conductor.xhtml.toc.param__**

    Pass parameters to the XSLT step that generates the XHTML table of contents \(TOC\).

-   **__dita.xsl.html.cover__**

    Overrides the default HTML cover page generation process.

-   **__dita.xsl.htmltoc__**

    Overrides the default XSLT step that generates the HTML table of contents \(TOC\).

-   **__dita.xsl.xhtml__**

    Overrides the default HTML or XHTML transformation, including HTML Help and Eclipse Help. The referenced file is integrated directly into the XSLT step that generates XHTML.


