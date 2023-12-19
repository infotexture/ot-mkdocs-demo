# PDF parameters

Certain parameters are specific to the PDF transformation.

-   **__args.artlbl__**

    Specifies whether to generate a label for each image; the label will contain the image file name. The allowed values are yes and no; the default value is no.

-   **__args.bookmap-order__**

    Specifies if the frontmatter and backmatter content order is retained in bookmap. The allowed values are retain and discard; the default value is discard.

-   **__args.bookmark.style__**

    Specifies whether PDF bookmarks are by default expanded or collapsed. The allowed values are EXPANDED and COLLAPSE.

-   **__args.chapter.layout__**

    Specifies whether chapter level TOCs are generated. The allowed values are MINITOC and BASIC; the default value is MINITOC.

-   **__args.fo.userconfig__**

    Specifies the user configuration file for FOP.

-   **__args.xsl.pdf__**

    Specifies an XSL file that is used to override the default XSL transformation.

    You must specify the fully qualified file name.

-   **__axf.cmd__**

    Specifies the path to the Antenna House Formatter executable.

-   **__axf.opt__**

    Specifies the user configuration file for Antenna House Formatter.

-   **__custom.xep.config__**

    Specifies the user configuration file for RenderX.

-   **__customization.dir__**

    Specifies the customization directory.

-   **__maxJavaMemory__**

    Specifies the amount of memory allocated to the RenderX process.

-   **__org.dita.index.skip__**

    Disable index processing. The allowed values are yes and no; the default value is no.

    Up until DITA-OT 3.4, indexing code was provided in the PDF plug-in and only available for PDF output. In version 3.4 and above, indexing is provided by a separate plug-in to allow other transformations to access the results.

    If you have overridden PDF index processing via the `transform.topic2fo` target in the past, you can set the **org.dita.index.skip** property to yes and re-enable the `transform.topic2fo.index` target with `<feature extension="depend.org.dita.pdf2.index" value="transform.topic2fo.index"/>` in your plug-in configuration.

-   **__org.dita.pdf2.chunk.enabled__**

    Enables chunk attribute processing. The following values are supported:

    -   true – Enables chunk processing
    -   false \(default\) – Disables chunk processing
-   **__org.dita.pdf2.i18n.enabled__**

    Enables internationalization \(I18N\) font processing to provide per-character font selection for FO renderers that do not support the `font-selection-strategy` property \(such as Apache FOP\).

    When this feature is enabled, DITA-OT uses a font mapping process that takes the content language into consideration. The mapping process uses configuration files for each language to define characters that should be rendered with certain logical fonts, and font mappings that associate each logical font to physical font files.

    The following values are allowed:

    -   true \(default\) — Enables font mapping
    -   false — Disables font mapping
    **Tip:** If you don’t use custom character mappings, turning off font mapping makes it easier to define custom fonts simply by changing font names in the XSL attributes files of your custom PDF plug-in. For details, see [Font configuration in PDF2](http://www.elovirta.com/2016/02/18/font-configuration-in-pdf2.html).

-   **__outputFile.base__**

    Specifies the base file name of the generated PDF file.

    By default, the PDF file uses the base filename of the input `.ditamap` file.

-   **__pdf.formatter__**

    Specifies the XSL processor. The following values are supported:

    -   xep – RenderX XEP Engine
    -   ah – Antenna House Formatter
    -   fop \(default\) – Apache FOP


-   **__publish.required.cleanup__**

    Specifies whether draft-comment and required-cleanup elements are included in the output. The allowed values are yes, no, yes, and no.

    The default value is the value of the **args.draft** parameter. Corresponds to the XSLT parameter **publishRequiredCleanup**.

    **Note:** This parameter is deprecated in favor of the **args.draft** parameter.

-   **__theme__**

    Theme configuration file.

-   **__xep.dir__**

    RenderX installation directory.


**Related information**  


[PDF transformation](../topics/dita2pdf.md)

[Common parameters](../parameters/parameters-base.md)

