# HTML-based output parameters

Certain parameters apply to all HTML-based transformation types: HTML5, XHTML, HTML Help, and Eclipse help. 

-   **__args.artlbl__**

    Specifies whether to generate a label for each image; the label will contain the image file name. The allowed values are yes and no; the default value is no.

-   **__args.copycss__**

    Specifies whether to copy the custom .css file to the output directory. The allowed values are yes and no; the default value is no.

    If an external process will copy your custom .css file to the output directory, leave this parameter unset \(or set it to no\). If DITA-OT should copy the file when generating output, set it to yes.

-   **__args.css__**

    Specifies the name of a custom .css file.

    The value of this parameter should be only the file name. The absolute path to the parent directory should be specified with **args.cssroot**.

-   **__args.csspath__**

    Specifies the **destination** directory to which .css files are copied \(relative to the output directory\).

    Corresponds to the XSLT parameter **CSSPATH**.

    DITA-OT will copy the file **to** this location.

    **Tip:** If **args.csspath** is not set, the custom CSS file \(and the default CSS files\) will be copied to the root level of the output folder. To copy CSS files to an output subfolder named `css`, set **args.csspath** to css.

-   **__args.cssroot__**

    Specifies the **source** directory that contains the custom .css file.

    DITA-OT will copy the file **from** this location.

    **Important:** Enter the absolute path to the parent directory of the custom CSS file specified with **args.css**.

-   **__args.dita.locale__**

    Specifies the language locale file to use for sorting index entries.

    **Note:** This parameter is not available for the XHTML transformation.

-   **__args.eclipse.provider__**

    Specifies the name of the person or organization that provides the Eclipse help.

-   **__args.eclipse.symbolic.name__**

    Specifies the symbolic name \(aka plugin ID\) in the output for an Eclipse Help project.

-   **__args.eclipse.version__**

    Specifies the version number to include in the output.

-   **__args.eclipsehelp.country__**

    Specifies the region for the language that is specified by the args.

-   **__args.eclipsehelp.jar.name__**

    Specifies that the output should be zipped and returned using this name.

-   **__args.eclipsehelp.language__**

    Specifies the base language for translated content, such as en for English.

-   **__args.ftr__**

    Specifies an XML file that contains content for a running footer.

    Corresponds to the XSLT parameter **FTR**.

    **Note:** The footer file should be specified using an absolute path and must contain valid XML. A common practice is to place all content into a `<div>` element. In HTML5 output, the footer file contents will be wrapped in an HTML5 `<footer>` element with the `@role` attribute set to contentinfo.

-   **__args.gen.default.meta__**

    Generate metadata for parental control scanners, meta elements with name="security" and name="Robots". The allowed values are yes and no; the default value is no.

    Corresponds to the XSLT parameter **genDefMeta**.

-   **__args.hdf__**

    Specifies an XML file that contains content to be placed in the document head.

    The contents of the header file will be inserted in the `<head>` element of the generated HTML files.

    **Tip:** The header file should be specified using an absolute path and must contain valid XML. If you need to insert more than one element into the HTML page head, wrap the content in a `<div>` element. The division wrapper in the header file will be discarded when generating HTML files, and the contents will be inserted into each page head.

-   **__args.hdr__**

    Specifies an XML file that contains content for a running header.

    Corresponds to the XSLT parameter **HDR**.

    **Note:** The header file should be specified using an absolute path and must contain valid XML. A common practice is to place all content into a `<div>` element. In HTML5 output, the contents of the header file will be wrapped in an HTML5 `<header>` element with the `@role` attribute set to banner.

-   **__args.hide.parent.link__**

    Specifies whether to hide links to parent topics in the HTML or XHTML output. The allowed values are yes and no; the default value is no.

    Corresponds to the XSLT parameter **NOPARENTLINK**.

    **Note:** This parameter is deprecated in favor of the **args.rellinks** parameter.

-   **__args.htmlhelp.includefile__**

    Specifies the name of a file that you want included in the HTML Help.

-   **__args.indexshow__**

    Specifies whether the content of &lt;indexterm&gt; elements are rendered in the output. The allowed values are yes and no; the default value is no.

-   **__args.outext__**

    Specifies the file extension for HTML or XHTML output.

    Corresponds to the XSLT parameter **OUTEXT**.

-   **__args.xhtml.classattr__**

    Specifies whether to include the DITA class ancestry inside the XHTML elements. The allowed values are yes and no; the default value is yes.

    For example, the `<prereq>` element \(which is specialized from `<section>`\) would generate `class="section prereq"`. Corresponds to the XSLT parameter **PRESERVE-DITA-CLASS**.

    **Note:** Beginning with DITA-OT release 1.5.2, the default value is yes. For release 1.5 and 1.5.1, the default value was no.

-   **__args.xhtml.contenttarget__**

    Specifies the value of the @target attribute on the &lt;base&gt; element in the TOC file.

-   **__args.xhtml.toc__**

    Specifies the base name of the TOC file.

-   **__args.xhtml.toc.class__**

    Specifies the value of the @class attribute on the &lt;body&gt; element in the TOC file.

-   **__args.xhtml.toc.xsl__**

    Specifies a custom XSL file to be used for TOC generation.

-   **__args.xsl__**

    Specifies a custom XSL file to be used instead of the default XSL transformation.

    The parameter must specify a fully qualified file name.


**Related information**  


[Eclipse help transformation](../topics/dita2eclipsehelp.md)

[HTML help transformation](../topics/dita2htmlhelp.md)

[XHTML transformation](../topics/dita2xhtml.md)

[Setting parameters for custom HTML](../topics/html-customization-parameters.md)

[HTML5 transformation](../topics/dita2html5.md)

[Bundling CSS in a custom HTML plug-in](../topics/html-customization-plugin-bundle-css.md)

[Embedding web fonts in HTML output](../topics/html-customization-plugin-webfont.md)

[Inserting JavaScript in generated HTML](../topics/html-customization-plugin-javascript.md)

[Eclipse Help parameters](../parameters/parameters-eclipsehelp.md)

[HTML5 parameters](../parameters/parameters-html5.md)

[Microsoft Compiled HTML Help parameters](../parameters/parameters-htmlhelp.md)

[XHTML parameters](../parameters/parameters-xhtml.md)

