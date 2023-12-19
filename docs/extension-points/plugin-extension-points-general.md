# General extension points

These extension points enable you to extend DITA-OT. You can add Ant targets or imports; add a Java library to the **classpath** parameter; add a new transformation type; extend a catalog file; add new diagnostic messages, and more.

-   **__ant.import__**

    Adds an Ant import to the main Ant build file.

-   **__dita.conductor.lib.import__**

    Adds a Java library to the DITA-OT classpath.

-   **__dita.conductor.target__**

    Adds an Ant import to the main Ant build file.

    **Attention:** This extension point is deprecated; use `ant.import` instead.

-   **__dita.conductor.target.relative__**

    Adds an Ant import to the main Ant build file.

    **Tip:** As of DITA-OT 3.0, the `ant.import` extension point can be used instead.

-   **__dita.conductor.transtype.check__**

    Adds a new value to the list of valid transformation types.

    **Tip:** This extension point is still supported for backwards compatibility, but since DITA-OT 2.1, any new customizations should instead use the `<transtype>` element in the [Plug-in descriptor file](../topics/plugin-configfile.md) to define a new transformation.

-   **__dita.specialization.catalog__**

    Adds the content of a catalog file to the main DITA-OT catalog file.

    **Attention:** This extension point is deprecated; use `dita.specialization.catalog.relative` instead.

-   **__dita.specialization.catalog.relative__**

    Adds the content of a catalog file to the main DITA-OT catalog file.

-   **__dita.transtype.print__**

    Defines a transformation as a print type.

-   **__dita.xsl.messages__**

    Adds new diagnostic messages to DITA-OT.

-   **__org.dita.pdf2.catalog.relative__**

    Adds the content of a catalog file to the main catalog file for the PDF plug-in.


**Related information**  


[Extension points in org.dita.base](../extension-points/extension-points-in-org.dita.base.md)

