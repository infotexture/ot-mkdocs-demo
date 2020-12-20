# Extension points in `org.dita.html5`

In addition to the extension points provided by common processing and those shared by with other HTML-based transformations, the `org.dita.html5` plug-in provides extension points that are specific to the HTML5 transformation. 

-   **dita.conductor.html5.param**

    Pass parameters to the HTML5 transformation.

-   **dita.conductor.html5.toc.param**

    Pass parameters to the XSLT step that generates the HTML5 table of contents \(TOC\).

-   **dita.xsl.html5**

    Overrides the default HTML5 transformation. The referenced file is integrated directly into the XSLT step that generates HTML5.

-   **dita.xsl.html5.cover**

    Overrides the default HTML5 cover page generation process.

-   **dita.xsl.html5.toc**

    Overrides the default XSLT step that generates the HTML5 table of contents \(TOC\).


