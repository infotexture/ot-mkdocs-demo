# Migrating to release 3.7

DITA-OT 3.7 includes stable IDs in re-used content, a common variable format for generated text strings, and an updated preview of features for the latest draft of the upcoming DITA 2.0 standard, such as the new “combine” chunk action, the `titlealt` element, and the alternative titles domain.

**Note:** This topic provides a summary of changes in DITA-OT 3.7 that may require modifications to custom stylesheets or plug-ins. For more information on changes in this release, see the [DITA-OT 3.7 Release Notes](https://www.dita-ot.org/3.7/release-notes/).

## Common format for generated text

Prior to DITA-OT 3.7, there were two different XML structures for adding or modifying generated text \(gentext\). The base plug-in **org.dita.base** and any custom overrides defined via the dita.strings.xsl extension point used a root element `strings`, with individual strings in `str` elements with `@name` attributes. This format was previously used for HTML, and all other output formats except PDF.

```
<?xml version="1.0" encoding="utf-8"?>
<strings xml:lang="en-US">
  <str name="String1">English generated text</str>
</strings>
```

The PDF plug-in **org.dita.pdf2** used a root element `vars` with an XML namespace, and strings in `variable` elements with `@id` attributes.

```
<?xml version="1.0" encoding="UTF-8"?>
<vars xmlns="http://www.idiominc.com/opentopic/vars">
  <variable id="String1">English generated text</variable>
</vars>
```

Starting with DITA-OT 3.7, these structures have been deprecated and replaced with a new unified format. All files now use `variables` as the root element, with the `variable` elements previously used in PDF strings. The new format supports the XSL parameters used by the earlier PDF strings format to pass dynamic information such as chapter numbers or figure titles.

```
<?xml version="1.0" encoding="UTF-8"?>
<variables>
  <variable id="String1">English generated text</variable>
</variables>
```

The old formats are still supported, but plug-in developers should update any generated text files to reflect the new structure, as support for the old formats may be removed in a future release. [\#3817](https://github.com/dita-ot/dita-ot/issues/3817)

## CSS precedence

The order of elements in the `head` element of the HTML template files was changed to facilitate overrides. The common CSS stylesheets and any custom CSS files specified via args.css now come **after** the contents of the custom header file specified via args.hdf. This change better supports use cases in which the custom header file is used to insert references to external CSS stylesheets for frameworks like [Bootstrap](https://getbootstrap.com/docs/5.0/getting-started/introduction/#css). In previous versions of DITA-OT, framework styles took precedence over any equivalent rules in the user’s custom stylesheet. This change allows rules in custom CSS files specified via args.css to override any of the framework styles as necessary.

## Deprecated legacy `gen-user` templates

The legacy `gen-user` templates that were originally used to add content to the `head` element have been deprecated and will be removed in a future release. For each of these templates, parameter-based customizations are available that can be used to specify files that contain content that extends the default processing. [\#3835](https://github.com/dita-ot/dita-ot/issues/3835)

-   `gen-user-head` → use args.hdf instead
-   `gen-user-header` → use args.hdr
-   `gen-user-footer` → use args.ftr
-   `gen-user-scripts` → use args.hdf
-   `gen-user-styles` → use args.css

## Ancestor links

The mappull processing step has changed how related links are generated with args.rellinks. Starting in 3.7, noparent will not generate any ancestor links and nofamily will not generate sibling, cousin, ancestor, or descendant links.

Prior to 3.7, args.rellinks=all did not actually include all links. Now it will. As in previous versions, the default value for PDF output is nofamily, and other output formats include all link roles except `ancestor` links.

The default processing sets the internal Ant property include.rellinks to `#default parent child sibling friend next previous cousin descendant sample external other`.

## ToC navigation role

Table of contents navigation in HTML5 output used a `nav` element with the ARIA `@role` attribute set to `toc`. Certain accessibility tools flagged this as an error. The invalid role has been replaced with the `navigation` landmark role. A new `toc` class allows custom CSS styles to target the ToC navigation. CSS rules that use the `nav[role='toc']` selector can be simplified to `nav.toc`.

## Common attributes mode

A `commonattributes` mode was added to the HTML5, PDF, and XHTML plug-ins to allow for easier extension. This is a backwards compatible change, however, existing plug-ins should be changed to use the new `commonattributes` mode.

```language-xml
<xsl:template name="commonattributes">
  <!-- whole copy of commonattributes named template with customizations -->
</xsl:template>
```

```language-xml
<xsl:template match="@* | node()" mode="commonattributes">
  <xsl:param name="default-output-class" as="xs:string*"/>
  <xsl:next-match>
    <xsl:with-param name="default-output-class" select="$default-output-class"/>
  </xsl:next-match>
  <!-- customizations -->
</xsl:template>
```

## XSL modes

The HTML5 stylesheets were updated to use XSL modes instead of named templates.

This is a backwards compatible change, however, existing plug-ins should be changed to use modes instead of named templates for:

-   `copyright`
-   `gen-endnotes`
-   `generateDefaultMeta`
-   `generateCssLinks`
-   `generateChapterTitle`
-   `processHDF`
-   `generateBreadcrumbs`
-   `processHDR`
-   `processFTR`
-   `generateCharset`

