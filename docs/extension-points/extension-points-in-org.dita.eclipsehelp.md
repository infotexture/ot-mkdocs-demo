# Extension points in `org.dita.eclipsehelp`

Certain extension points are specific to the Eclipse Help transformation. 

-   **__dita.conductor.eclipse.toc.param__**

    Pass parameters to the XSLT step that generates the Eclipse Help table of contents \(TOC\).

-   **__dita.map.eclipse.index.pre__**

    Runs an Ant target before the Eclipse index extraction process.

-   **__dita.xsl.eclipse.plugin__**

    Overrides the default XSLT step that generates the `plugin.xml` file for Eclipse Help.

-   **__dita.xsl.eclipse.toc__**

    Overrides the default XSLT step that generates the Eclipse Help table of contents \(TOC\).


