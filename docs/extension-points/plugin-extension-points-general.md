# General extension points

These extension points enable you to extend DITA-OT. You can add Ant targets or imports; add a Java library to the classpath parameter; add a new transformation type; extend a catalog file; add new diagnostic messages, and more.

-   **ant.import**

    Adds an Ant import to the main Ant build file.

-   **dita.conductor.lib.import**

    Adds a Java library to the DITA-OT classpath.

-   **dita.conductor.target**

    Adds an Ant import to the main Ant build file.

    **Attention:** This extension point is deprecated; use `ant.import` instead.

-   **dita.conductor.target.relative**

    Adds an Ant import to the main Ant build file.

    **Tip:** As of DITA-OT 3.0, the `ant.import` extension point can be used instead.

-   **dita.conductor.transtype.check**

    Adds a new value to the list of valid transformation types.

    **Tip:** This extension point is still supported for backwards compatibility, but since DITA-OT 2.1, any new customizations should instead use the `transtype` element in the [Plug-in descriptor file](../topics/plugin-configfile.md) to define a new transformation.

-   **dita.specialization.catalog**

    Adds the content of a catalog file to the main DITA-OT catalog file.

    **Attention:** This extension point is deprecated; use `dita.specialization.catalog.relative` instead.

-   **dita.specialization.catalog.relative**

    Adds the content of a catalog file to the main DITA-OT catalog file.

-   **dita.transtype.print**

    Defines a transformation as a print type.

-   **dita.xsl.messages**

    Adds new diagnostic messages to DITA-OT.

-   **org.dita.pdf2.catalog.relative**

    Adds the content of a catalog file to the main catalog file for the PDF plug-in.


**Related information**  


[Extension points in org.dita.base](../extension-points/extension-points-in-org.dita.base.md)

