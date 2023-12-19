# HTML5 parameters

The HTML5 transformation shares common parameters with other HTML-based transformations and provides additional parameters that are specific to HTML5 output. 

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

    Specifies whether to hide links to parent topics in the HTML5 output. The allowed values are yes and no; the default value is no.

    Corresponds to the XSLT parameter **NOPARENTLINK**.

    **Note:** This parameter is deprecated in favor of the **args.rellinks** parameter.

-   **__args.html5.classattr__**

    Specifies whether to include the DITA class ancestry inside the HTML5 elements. The allowed values are yes and no; the default value is yes.

-   **__args.html5.contenttarget__**

    Specifies the value of the @target attribute on the &lt;base&gt; element in the TOC file.

-   **__args.html5.toc__**

    Specifies the base name of the TOC file.

-   **__args.html5.toc.class__**

    Specifies the value of the @class attribute on the &lt;body&gt; element in the TOC file.

-   **__args.html5.toc.xsl__**

    Specifies a custom XSL file to be used for TOC generation.

-   **__args.indexshow__**

    Specifies whether the content of &lt;indexterm&gt; elements are rendered in the output. The allowed values are yes and no; the default value is no.

-   **__args.outext__**

    Specifies the file extension for HTML5 output.

    Corresponds to the XSLT parameter **OUTEXT**.

-   **__args.xsl__**

    Specifies a custom XSL file to be used instead of the default XSL transformation.

    The parameter must specify a fully qualified file name.

-   **__html5.toc.generate__**

    Generate TOC file from the DITA map. The allowed values are yes and no; the default value is yes.

-   **__nav-toc__**

    Specifies whether to generate a table of contents \(ToC\) in the HTML5 `<nav>` element of each page. The navigation can then be rendered in a sidebar or menu via CSS.

    The following values are supported:

    -   none \(default\) – No table of contents will be generated
    -   partial – Include the current topic in the ToC along with its parents, siblings and children
    -   full – Generate a complete ToC for the entire map

**Related information**  


[HTML5 transformation](../topics/dita2html5.md)

[Setting parameters for custom HTML](../topics/html-customization-parameters.md)

[HTML-based output parameters](../parameters/parameters-base-html.md)

