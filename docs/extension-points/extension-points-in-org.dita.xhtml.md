# Extension points in `org.dita.xhtml`

The `org.dita.xhtml` plug-in provides shared extension points that can be used to modify processing in HTML-based transformation types such as Eclipse help, HTML Help, and XHTML. 

-   **dita.conductor.html.param**

    Pass parameters to the HTML and HTML Help transformations.

-   **dita.conductor.xhtml.param**

    Pass parameters to the XHTML and Eclipse Help transformations.

-   **dita.conductor.xhtml.toc.param**

    Pass parameters to the XSLT step that generates the XHTML table of contents \(TOC\).

-   **dita.xsl.html.cover**

    Overrides the default HTML cover page generation process.

-   **dita.xsl.htmltoc**

    Overrides the default XSLT step that generates the HTML table of contents \(TOC\).

-   **dita.xsl.xhtml**

    Overrides the default HTML or XHTML transformation, including HTML Help and Eclipse Help. The referenced file is integrated directly into the XSLT step that generates XHTML.


