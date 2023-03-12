# DITA Open Toolkit 4.0 Release Notes

DITA Open Toolkit 4.0.2 is a maintenance release that fixes issues reported in DITA-OT 4.0, which includes a new plug-in for easier PDF customization, project file improvements, updates to LwDITA processing, and support for the split chunking feature in the latest drafts of the upcoming DITA 2.0 standard.

DITA-OT releases follow [semantic versioning](https://semver.org) guidelines. Version numbers use the `major.minor.patch` syntax, where major versions may include incompatible API changes, minor versions add functionality in a backwards-compatible manner and patch versions are maintenance releases that include backwards-compatible bug fixes.

**Tip:** Download the dita-ot-4.0.2.zip package from the project website at [dita-ot.org/download](https://www.dita-ot.org/download).

## Requirements: Java 17

DITA-OT 4.0 is designed to run on Java version 17 or later and built and tested with the Open Java Development Kit \(OpenJDK\). Compatible Java distributions are available from multiple sources:

-   You can download the Oracle JRE or JDK from [oracle.com/java](https://www.oracle.com/java/technologies/downloads/) under commercial license.
-   Eclipse Temurin is the free OpenJDK distribution available from [adoptium.net](https://adoptium.net/temurin/releases/?version=17).
-   Free OpenJDK distributions are also provided by [Amazon Corretto](https://aws.amazon.com/corretto/), [Azul Zulu](https://www.azul.com/downloads/), and [Red Hat](https://developers.redhat.com/products/openjdk/download).

**Note:** The Java virtual machine is generally backwards compatible, so class files built with earlier versions should still run correctly with Java 17 and DITA-OT 4.0. If your DITA-OT installation contains plug-ins with custom Java code, you may need to recompile these with Java 17 — but in most cases, this step should not be necessary.

## DITA-OT 4.0.2 released February 18, 2023

DITA Open Toolkit 4.0.2 is a maintenance release that includes the following bug fixes.

-   Earlier versions of DITA-OT did not respect key references defined on long descriptions within image elements. Processing has been updated to ensure that `@keyref` attributes on `longdescref` elements are resolved to the resource defined by the `@href` attribute on the key. [\#4071](https://github.com/dita-ot/dita-ot/issues/4071), [\#4080](https://github.com/dita-ot/dita-ot/issues/4080)
-   If `@copy-to` attributes were used to create duplicate versions of topics, previous versions did not resolve key references to content inside the topic copies correctly. Key reference processing has been corrected to ensure that topic IDs for copied topics are properly adjusted when calculating link targets. [\#4076](https://github.com/dita-ot/dita-ot/issues/4076), [\#4110](https://github.com/dita-ot/dita-ot/issues/4110)
-   In certain cases, when a context map resource was passed to the dita command with the --resource option or the args.resources parameter, the resource map was overwritten with its temporary version from preprocessing. These maps are now copied and processed to the temporary files folder instead of being overwritten in-place, and the key values they contain are correctly resolved from the copies in the temporary folder. [\#4104](https://github.com/dita-ot/dita-ot/issues/4104), [\#4112](https://github.com/dita-ot/dita-ot/issues/4112)
-   In earlier versions, the DITA-OT logging configuration mistakenly enabled full debug logging for all Java packages in any of the installed plug-ins. This error has been corrected to preserve the default `INFO` level for custom plug-ins, and only enable debug logging for Java code in DITA-OT itself. [\#4106](https://github.com/dita-ot/dita-ot/issues/4106), [\#4114](https://github.com/dita-ot/dita-ot/issues/4114)
-   Content key references in map titles were not resolved if they pointed to phrase elements that contained another `ph` element. Key references are now handled correctly, even when `@conkeyref` targets contain nested phrase elements. [\#4117](https://github.com/dita-ot/dita-ot/issues/4117), [\#4120](https://github.com/dita-ot/dita-ot/issues/4120)
-   Obsolete Travis configuration files have been removed from the DITA-OT repository. [\#4118](https://github.com/dita-ot/dita-ot/issues/4118)

For additional information on the issues resolved since the previous release, see the [4.0.2 milestone](https://github.com/dita-ot/dita-ot/issues?q=milestone%3A4.0.2+is%3Aclosed) and [changelog](https://github.com/dita-ot/dita-ot/compare/4.0.1...4.0.2) on GitHub.

## DITA-OT 4.0.1 released December 9, 2022

DITA Open Toolkit 4.0.2 is a maintenance release that includes the following bug fixes.

-   The `place-tbl-lbl` template that was originally used to define table titles in XHTML has been deprecated in HTML5 processing and will be removed in a future release. This template was carried over from XHTML code \(which still has a copy that is used\), but the copy in HTML5 is not called. [\#3435](https://github.com/dita-ot/dita-ot/issues/3435), [\#4056](https://github.com/dita-ot/dita-ot/issues/4056)
-   In earlier versions, the args.xhtml.toc.class and args.html5.toc.class properties did not work. HTML processing has been updated to ensure that the value of the `@class` attribute is correctly set on the `body` element in the table of contents \(TOC\) files generated for XHTML and HTML5 output. [\#4015](https://github.com/dita-ot/dita-ot/issues/4015), [\#4065](https://github.com/dita-ot/dita-ot/issues/4065)
-   The bundled Jackson data binding library was updated the latest version \(2.14.0\) to resolve a security vulnerability. [\#4016](https://github.com/dita-ot/dita-ot/issues/4016), [\#4058](https://github.com/dita-ot/dita-ot/issues/4058)
-   When link targets included index terms, PDF output generated by earlier versions added the text of the index entries to the end of cross-reference link text. Processing has been updated to correctly filter `indexterm` elements when computing the target text for `xref` elements. [\#4017](https://github.com/dita-ot/dita-ot/issues/4017), [\#4030](https://github.com/dita-ot/dita-ot/issues/4030)
-   In earlier releases, syntax diagrams with an `@id` attribute did not preserve the ID in HTML5 output. This is now fixed. [\#4021](https://github.com/dita-ot/dita-ot/issues/4021), [\#4057](https://github.com/dita-ot/dita-ot/issues/4057)
-   A spelling mistake has been corrected in the DOTX034E message that appears when unordered list items are cross-referenced without specifying link text. [\#4029](https://github.com/dita-ot/dita-ot/issues/4029)
-   In earlier versions, conditional processing did not work as expected when specialized attributes were used for flagging. The flagging module has been updated to work correctly with specialized attributes. [\#4043](https://github.com/dita-ot/dita-ot/issues/4043), [\#4053](https://github.com/dita-ot/dita-ot/issues/4053)

For additional information on the issues resolved since the previous release, see the [4.0.1 milestone](https://github.com/dita-ot/dita-ot/issues?q=milestone%3A4.0.1+is%3Aclosed) and [changelog](https://github.com/dita-ot/dita-ot/compare/4.0...4.0.1) on GitHub.

## DITA-OT 4.0 released November 12, 2022

DITA Open Toolkit Release 4.0 includes a new plug-in for easier PDF customization, project file improvements, updates to LwDITA processing, and support for the split chunking feature in the latest drafts of the upcoming DITA 2.0 standard.

### New PDF theme plug-in

DITA-OT 4.0 includes the `com.elovirta.pdf` plug-in, which extends the default PDF2 plug-in with a new theme parameter. The --theme option takes a path to a theme file and changes the styling of the PDF output without requiring changes to XSLT stylesheets.

Themes can be used to adjust basic settings like cover page images, page sizes, numbering, font properties, background colors and borders, spacing, and running content like page headers and footers.

To generate PDF output with a custom theme, pass the theme file to the dita command with the --theme option:

```syntax-bash
dita --project=samples/project-files/pdf.xml \
     --theme=path/to/custom-theme-file.yaml
```

**Tip:** For information on the available theming options and a sample YAML theme, see [PDF themes](../topics/pdf-themes.md).

### Project file improvements

-   The re-usable `publication` element in DITA-OT project files can now be overridden with additional parameters \(or modified parameter settings\) by adding new `param` elements to the referencing element. [\#3682](https://github.com/dita-ot/dita-ot/issues/3682), [\#3907](https://github.com/dita-ot/dita-ot/issues/3907)

    This allows common publications to be defined in one place, re-used in others, and overlaid with local variations when the common settings need to be adjusted in certain cases.

    ```
    <project xmlns="https://www.dita-ot.org/project">
      <publication transtype="html5" id="common-html5">
        <param name="nav-toc" value="partial"/>
      </publication>
      <deliverable>
        <context>
          <input href="root.ditamap"/>
        </context>
        <output href="./out"/>
        <publication idref="common-html5">
          <!-- Define publication-specific parameter settings -->
          <param name="nav-toc" value="full"/>
        </publication>
      </deliverable>
    </project>
    ```

-   The `publication` element in DITA-OT project files now supports nested `profile` elements. When both context and publication contain profiles, they are applied in order: publication profiles first, context profiles second. [\#3690](https://github.com/dita-ot/dita-ot/issues/3690), [\#3895](https://github.com/dita-ot/dita-ot/issues/3895)

    This allows publications to define filter criteria that are applied to the content of the individual publication \(in addition to those specified for the entire deliverable context\).

    ```
    <project xmlns="https://www.dita-ot.org/project">
      <deliverable name="Name" id="site">
        <context name="Site" id="site">
          <input href="site.ditamap"/>
          <profile>
            <ditaval href="site.ditaval"/>
          </profile>
        </context>
        <output href="./site"/>
        <publication transtype="html5" id="sitePub" name="Site">
          <profile>
            <!-- Define publication-specific filters -->
            <ditaval href="site-html5.ditaval"/>
          </profile>
        </publication>
      </deliverable>
    </project>
    ```


### Lightweight DITA and Markdown updates

The `org.lwdita` plug-in has been updated to version 3.3, which includes Markdown processing improvements.

-   DITA-OT 4.0 includes processing updates to reflect recent changes to the latest drafts of the LwDITA profile from OASIS
-   Add support for Markdown files without first-level headings
-   Better support for [Python-Markdown Attribute Lists](https://python-markdown.github.io/extensions/attr_list/)
-   Markdown input improvements:
    -   Improve subscript and superscript support
    -   Fix backslash escapes in code phrases \(applies only to `@format`=`markdown`, as MDITA does not support code phrases\)
    -   Add support for table spanning
-   In previous releases, standard Markdown syntax could be used to indicate a span of code by wrapping it with backtick quotes \(```\). These constructs were converted to DITA `codeph` elements on import, and rendered as `code` elements in HTML output. This support has been removed from MDITA processing to align with LwDITA, which does not support code phrase markup.

### Updated DITA 2.0 preview

In addition to the [DITA 2.0 preview support](../reference/dita-v2-0-support.md) provided in previous releases \(3.5, 3.6, and 3.7\), DITA-OT 4.0 includes updated processing support for the latest drafts of the DITA 2.0 DTD and RELAX NG grammar files from OASIS \(as of November 7, 2022\). [\#4040](https://github.com/dita-ot/dita-ot/issues/4040)

-   The new “split” chunk action can be used to break content into new output documents. [\#3942](https://github.com/dita-ot/dita-ot/issues/3942)

    When the `@chunk` attribute is set to `split` on a map, branch, or map reference, each topic from the referenced source document will be rendered as an individual document.

    **Note:** The new chunk action is only applied if the root map has a DITA 2.0 doctype, such as:

    `<!DOCTYPE map PUBLIC "-//OASIS//DTD DITA 2.0 Map//EN" "map.dtd">`

    If the root map uses an unversioned \(or 1.x\) doctype, DITA 1.3 processing will be applied, and 2.0 chunk actions will be ignored. With a 2.0 root map, any 1.3 chunk actions are ignored.


DITA documents that reference the draft grammar files can be parsed, and where features overlap with DITA 1.3, those features will work as expected.

**Note:** Other new or revised features proposed for DITA 2.0 are not yet supported. Additional features will be implemented in future versions of DITA-OT as the specification evolves.

### Code references now default to UTF-8 encoding

The default character set for code references has been changed from the system default encoding to UTF-8.

This allows a wider range of characters to be used without needing to specify the `@format` attribute on the `coderef` element as described in [character set definition](../reference/extended-functionality.md#coderef-charset) or change the default encoding in the [configuration.properties file](../parameters/configuration-properties-file.md). [\#4046](https://github.com/dita-ot/dita-ot/issues/4046)

**Note:** If you have code references that require a different encoding, use either of these mechanisms to specify the character set explicitly.

### Enhancements and changes

DITA Open Toolkit Release 4.0 includes the following enhancements and changes to existing features:

-   When [publishing with project files](../topics/using-project-files.md), separate temporary folders are now created for each deliverable in the project. This facilitates debugging and troubleshooting, as it makes it easier to inspect the temporary files that have been created for each deliverable. [\#3757](https://github.com/dita-ot/dita-ot/issues/3757), [\#3898](https://github.com/dita-ot/dita-ot/issues/3898)
-   The legacy attribute set reflection in PDF2 has been replaced with code that generates new attribute sets directly. This change is backwards-compatible as the old attribute set reflection code has been retained, but PDF2 now uses the new attribute set generation mechanism everywhere reflection was used. Custom plug-ins that still use reflection should be updated to the new approach, as the legacy code may be removed in a future version. [\#3827](https://github.com/dita-ot/dita-ot/issues/3827), [\#3829](https://github.com/dita-ot/dita-ot/issues/3829)
-   Attribute generation routines in XSLT stylesheets have been refactored from the old XSLT 1.0 style `xsl:value-of select="…"` to the modern XSLT 2 notation: `xsl:attribute select="…"/`. [\#3830](https://github.com/dita-ot/dita-ot/issues/3830)
-   Many Ant targets refer to `skip` properties that can be used to skip preprocessing steps. In earlier releases, these properties were not set or named consistently; these properties are now generated automatically with more consistent naming and behavior. [\#3851](https://github.com/dita-ot/dita-ot/issues/3851)
-   When an included file uses a character set that is neither the system default nor matches the explicit character set definition in the include, reading the file may fail. A new DOTJ084E error message makes it easier to debug character set encoding issues like this in source files. [\#3891](https://github.com/dita-ot/dita-ot/issues/3891)
-   Grammar caching and validation has been added for RELAX NG–based DITA topics and maps. Together these enhancements make publishing faster and more reliable for RNG-based content. [\#3253](https://github.com/dita-ot/dita-ot/issues/3253), [\#3661](https://github.com/dita-ot/dita-ot/issues/3661), [\#3926](https://github.com/dita-ot/dita-ot/issues/3926)
-   Many XSLT files have been updated to use `#current` for the processing mode. This simplifies the code and makes it easier to read and maintain. [\#3974](https://github.com/dita-ot/dita-ot/issues/3974)

### Bug fixes

DITA Open Toolkit Release 4.0 provides fixes for the following bugs:

-   In earlier releases, unexpected or invalid markup in a plugin.xml file might throw errors, but the installation would still show as successful. This has been fixed, and plug-in installation will now fail when the integration process does not work. [\#2641](https://github.com/dita-ot/dita-ot/issues/2641), [\#3825](https://github.com/dita-ot/dita-ot/issues/3825)
-   In earlier releases, the `@frame`=`"none"` attribute on tables was not properly handled for PDF output. This issue has been fixed, and the table border is now handled correctly. [\#3303](https://github.com/dita-ot/dita-ot/issues/3303), [\#3852](https://github.com/dita-ot/dita-ot/issues/3852), [\#3854](https://github.com/dita-ot/dita-ot/issues/3854)
-   In 3.7 and some earlier releases, including namespaced elements such as `m:math` or `svg:svg` in a topic that is chunked would result in build failures. The chunking process now handles these elements without errors. [\#3684](https://github.com/dita-ot/dita-ot/issues/3684)
-   The `FINALOUTPUTTYPE` XSLT parameter has been removed from maplinkImpl.xsl and mappullImpl.xsl; this parameter is a legacy of very early code and has never been used by DITA-OT. [\#4018](https://github.com/dita-ot/dita-ot/issues/4018)
-   In DITA-OT 3.7.4, publishing failed with an IllegalArgumentException when images were referenced with an HTTP URI scheme. Processing has been corrected to set the missing `@scope` attribute to `external` per [DITA 1.3 specification: The scope attribute](http://docs.oasis-open.org/dita/dita/v1.3/errata02/os/complete/part3-all-inclusive/langRef/attributes/thescopeattribute.html#thescopeattribute). [\#4032](https://github.com/dita-ot/dita-ot/issues/4032), [\#4039](https://github.com/dita-ot/dita-ot/issues/4039)

### Contributors

DITA Open Toolkit Release 4.0 includes [code contributions](https://github.com/dita-ot/dita-ot/graphs/contributors) by the following people:

1.  Jarno Elovirta
2.  Radu Coravu
3.  Robert D Anderson
4.  Toshihiko Makita
5.  Eric Sirois
6.  Chris Papademetrious
7.  Julien Lacour
8.  Roger Sheen

For the complete list of changes since the previous release, see the [changelog](https://github.com/dita-ot/dita-ot/compare/3.7.4...4.0) on GitHub.

### Documentation updates

The documentation for DITA Open Toolkit Release 4.0 provides corrections and improvements to existing topics, along with new information in the following topics:

-   [PDF themes](../topics/pdf-themes.md)
-   [Migrating to release 4.0](../topics/migrating-to-4.0.md)
-   [DITA 2.0 preview support](../reference/dita-v2-0-support.md)

For additional information on documentation issues resolved in DITA Open Toolkit Release 4.0, see the [4.0 milestone](https://github.com/dita-ot/docs/issues?q=milestone%3A4.0+is%3Aclosed) in the documentation repository.

DITA Open Toolkit Release 4.0 includes [documentation contributions](https://github.com/dita-ot/docs/graphs/contributors) by the following people:

1.  Roger Sheen
2.  Jarno Elovirta

For the complete list of documentation changes since the previous release, see the [changelog](https://github.com/dita-ot/docs/compare/3.7.4...4.0).

