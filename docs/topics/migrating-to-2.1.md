# Migrating to release 2.1

In DITA-OT 2.1, the `insertVariable` template was deprecated for PDF transformations and should be replaced with the `getVariable` template. Various `dita.**out.**map.*` targets have been deprecated in favor of updated `dita.map.*` equivalents.

**Note:** This topic provides a summary of changes in DITA-OT 2.1 that may require modifications to custom stylesheets or plug-ins. For more information on changes in this release, see the [DITA-OT 2.1 Release Notes](https://www.dita-ot.org/2.1/release-notes/).

The customFileUtils code used to handle input and output in earlier versions of DITA-OT has been replaced with the [Apache Commons IO](http://commons.apache.org/proper/commons-io/) utilities library.

## Deprecated targets

The following build targets have been deprecated and will be removed in an upcoming release:

-   The `help` target that includes a reference to the current DITA-OT version during the build process.

## Preprocessing

The following Ant properties and generated list files have been deprecated:

-   imagefile property and `image.list` file
-   htmlfile property and `html.list` file

The following pre-processing targets and extension points have been deprecated:

-   The `copy-subsidiary` target used to copy subsidiary files
-   The `copy-subsidiary-check` target used to check for subsidiary files
-   The depend.preprocess.copy-subsidiary.pre extension point used to insert an Ant target before the `copy-subsidiary` step in the pre-processing stage.

A newdita.parser extension point has been added to allow plug-ins to contribute a custom parser for DITA files. If a custom DITA parser is defined, the preprocessing routines will use it during the gen-list and debug-filter stages to output DITA XML.

## PDF

The following template has been deprecated:

-   `insertVariable`, use `getVariable` instead

Calls to that template will result in warnings in the build log.

To update your plug-in, make the following changes:

```
<xsl:call-template name="insertVariable**getVariable**">
  <xsl:with-param name="theVariableID**id**" select="var-id"/>
  <xsl:with-param name="theParameters**params**">
    params
  </xsl:with-param>
</xsl:call-template>
```

## HTML-based output formats

The keydefs variable and the following XSL parameters have been deprecated:

-   KEYREF-FILE
-   displaytext
-   keys
-   target

The following template modes have been deprecated:

-   `pull-in-title`
-   `common-processing-phrase-within-link`

## XHTML

The `dita.**out.**map.xhtml.toc` target has been deprecated and should be replaced with the updated `dita.map.xhtml.toc` equivalent.

Keydef processing has been removed from the XHTML rendering code. Keys are now resolved in one preprocessing step, whereas in earlier versions of DITA-OT, the XHTML code returned to the keydef.xml file to look up targets for phrase elements and pull in text when needed.

This change affects non-linking elements that can’t take `@href` attributes, such as `ph`, `keyword`, `cite`, `dt`, `term`, and `indexterm` \(when `$INDEXSHOW` is active\).

## HTMLHelp

The `dita.**out.**map.htmlhelp.*` targets have been deprecated and should be replaced with the updated `dita.map.htmlhelp.*` equivalents:

-   `dita.out.map.htmlhelp.hhp`, use `dita.map.htmlhelp.hhp` instead
-   `dita.out.map.htmlhelp.hhc`, use `dita.map.htmlhelp.hhc` instead
-   `dita.out.map.htmlhelp.hhk`, use `dita.map.htmlhelp.hhk` instead

## JavaHelp

The `dita.**out.**map.javahelp.*` targets have been deprecated and should be replaced with the updated `dita.map.javahelp.*` equivalents:

-   `dita.out.map.javahelp.toc`, use `dita.map.javahelp.toc` instead
-   `dita.out.map.javahelp.map`, use `dita.map.javahelp.map` instead
-   `dita.out.map.javahelp.set`, use `dita.map.javahelp.set` instead
-   `dita.out.map.javahelp.index`, use `dita.map.javahelp.index` instead

## OpenDocument Text

Support for the args.odt.img.embed parameter has been removed from OpenDocument Text transformations. The previous default behavior was to embed images as Base64-encoded text, but editors do not use this as a default. Instead, office packages such as LibreOffice will convert embedded images into linked images on opening and saving an ODT file.

