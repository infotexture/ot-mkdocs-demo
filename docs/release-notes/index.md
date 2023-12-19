# DITA Open Toolkit 4.1 Release Notes

DITA Open Toolkit 4.1.2 is a maintenance release that fixes issues reported in DITA-OT 4.1, which includes a new version of the Lightweight DITA plug-in with significant enhancements to Markdown processing, and updates for the latest DITA 2.0 draft standard.

DITA-OT releases follow [semantic versioning](https://semver.org) guidelines. Version numbers use the *major.minor.patch* syntax, where *major* versions may include incompatible API changes, *minor* versions add functionality in a backwards-compatible manner and *patch* versions are maintenance releases that include backwards-compatible bug fixes.

**Tip:** Download the `dita-ot-4.1.2.zip` package from the project website at [dita-ot.org/download](https://www.dita-ot.org/download).

## Requirements: Java 17

DITA-OT 4.1 is designed to run on Java version 17 or later and built and tested with the Open Java Development Kit \(OpenJDK\). Compatible Java distributions are available from multiple sources:

-   You can download the Oracle JRE or JDK from [oracle.com/java](https://www.oracle.com/java/technologies/downloads/) under commercial license.
-   Eclipse Temurin is the free OpenJDK distribution available from [adoptium.net](https://adoptium.net/temurin/releases/?version=17).
-   Free OpenJDK distributions are also provided by [Amazon Corretto](https://aws.amazon.com/corretto/), [Azul Zulu](https://www.azul.com/downloads/), and [Red Hat](https://developers.redhat.com/products/openjdk/download).

**Note:** The Java virtual machine is generally backwards compatible, so class files built with earlier versions should still run correctly with Java 17 and DITA-OT 4.1. If your DITA-OT installation contains plug-ins with custom Java code, you may need to recompile these with Java 17 — but in most cases, this step should not be necessary.

## DITA-OT 4.1.2

DITA Open Toolkit 4.1.2 is a maintenance release that includes the following bug fixes.

-   Various issues in map-first preprocessing have been resolved in this release. [\#4237](https://github.com/dita-ot/dita-ot/issues/4237)
    -   Earlier versions failed to expand content references that were specified in key definitions. In `preprocess2`, content references are now expanded before key references to ensure that all topics are available when the map is processed. [\#2420](https://github.com/dita-ot/dita-ot/issues/2420), [\#4258](https://github.com/dita-ot/dita-ot/issues/4258), [\#4261](https://github.com/dita-ot/dita-ot/issues/4261)
    -   Key references to duplicate topics created via `@copy-to` attributes caused builds to fail. This issue was initially resolved for the original preprocessing routine in DITA-OT 3.1.1. The original source information is now also correctly recorded for copy-to targets in `preprocess2`, allowing builds to continue. [\#3007](https://github.com/dita-ot/dita-ot/issues/3007), [\#3015](https://github.com/dita-ot/dita-ot/issues/3015)
    -   Earlier versions failed to catch certain validation errors in `preprocess2`. Map-first preprocessing has been updated to validate files correctly. [\#3281](https://github.com/dita-ot/dita-ot/issues/3281)
    -   In DITA-OT 3.5 to 4.1, map-first preprocessing failed to report unresolved content references to topics that were not referenced in the map, and any key references they contained were not expanded. In the past, this issue could be avoided by adding content reference targets to the map with the `@processing-role` attribute set to `resource-only`, but this workaround is no longer necessary. Unresolved references should now be reported, and keys expanded even if the target topics are not referenced in the map. [\#3446](https://github.com/dita-ot/dita-ot/issues/3446), [\#3546](https://github.com/dita-ot/dita-ot/issues/3546)
    -   Map-first preprocessing set incorrect values for the `path2project`, `path2project-uri`, and `path2rootmap-uri` processing instructions. In `preprocess2`, they are now set with correct values that match the original preprocess output. [\#3514](https://github.com/dita-ot/dita-ot/issues/3514), [\#4252](https://github.com/dita-ot/dita-ot/issues/4252)
    -   The map-first preprocessing test code has been simplified to use the same expected output for the original preprocessing routines and `preprocess2`. [\#4268](https://github.com/dita-ot/dita-ot/issues/4268)
-   Network file URI validation has been fixed to allow builds to continue when cross-references point to invalid URIs. Up until DITA-OT 3.6, the non-standard 2-slash format could be used to represent the server name in Windows UNC filenames such as `\\server\folder\file.pdf` using the Authority part of the URI as `file://server/folder/file.pdf`. Recent versions of DITA-OT required the correct 3-slash notation with an explicitly empty authority component \(`file:///server/folder/file.pdf`\), or builds would fail. Validation has been relaxed to restore support for the 2-slash format. [\#3718](https://github.com/dita-ot/dita-ot/issues/3718), [\#4255](https://github.com/dita-ot/dita-ot/issues/4255)
-   Chunk-to-content publishing failed on DITA map files whose paths included spaces. The chunk map reader module now normalizes map file paths to allow publishing to continue in these cases. [\#4064](https://github.com/dita-ot/dita-ot/issues/4064), [\#4257](https://github.com/dita-ot/dita-ot/issues/4257)
-   The HTML5 plug-in has been updated to remove the remaining inline style attributes that prevented custom plug-ins from overriding the monospace font presentation of teletype `<tt>` elements. These changes move the default teletype styling to CSS to allow users to override the presentation in custom stylesheets. The output is visually equivalent to the results generated by previous toolkit versions. [\#4254](https://github.com/dita-ot/dita-ot/issues/4254), [\#4267](https://github.com/dita-ot/dita-ot/issues/4267)

    **Important:** In publishing environments that do not use the default common CSS files, these styles may need to be implemented in custom stylesheets.

-   Test coverage has been improved to include unit tests for preprocessing, integration tests for subject schemes, and unit tests for cascading metadata in duplicate topicrefs. [\#4259](https://github.com/dita-ot/dita-ot/issues/4259), [\#4264](https://github.com/dita-ot/dita-ot/issues/4264), [\#4280](https://github.com/dita-ot/dita-ot/issues/4280)
-   In earlier versions, cross-references or other links to titles that contained footnotes included the footnote text. For a link to a target element that has no explicit link text, DITA-OT computes default link text from the target element. Link text computation now ignores any `<fn>` elements it encounters, so the link shows only the text from the `<title>` element. [\#4269](https://github.com/dita-ot/dita-ot/issues/4269), [\#4276](https://github.com/dita-ot/dita-ot/issues/4276)
-   When maps point to the same resource in multiple topic references with different navigation titles \(or other topic metadata\), older versions of DITA-OT used the metadata from the first reference for all subsequent instances. The original code was written to cascade metadata within the map and also collect metadata to be pushed to topics. This code worked when each topic was only referenced once. When there were duplicates, only the first topic reference got the correct cascaded metadata; the second reference was processed with the cascaded metadata, but also with the metadata from the first topicref. The code has been refactored to separate metadata cascading within maps from the collection of metadata to push to topics, so subsequent references to the same resource now retain the correct metadata for each instance. [\#4275](https://github.com/dita-ot/dita-ot/issues/4275), [\#4283](https://github.com/dita-ot/dita-ot/issues/4283), [\#4284](https://github.com/dita-ot/dita-ot/issues/4284)
-   The bundled XML Resolver has been upgraded to version 5.2.1, which no longer fails on invalid URI characters like spaces or Windows backslashes, and now also runs in environments with a restrictive security manager. [\#4274](https://github.com/dita-ot/dita-ot/issues/4274), [\#4279](https://github.com/dita-ot/dita-ot/issues/4279)

For additional information on the issues resolved since the previous release, see the [4.1.2 milestone](https://github.com/dita-ot/dita-ot/issues?q=milestone%3A4.1.2+is%3Aclosed) and [changelog](https://github.com/dita-ot/dita-ot/compare/4.1.1...4.1.2) on GitHub.

## DITA-OT 4.1.1 released July 20, 2023

DITA Open Toolkit 4.1.1 is a maintenance release that includes the following bug fixes.

-   In previous releases, there were some cases in which a `<desc>` element inside an `<xref>` or `<link>` element was not annotated with the expected `ditaot usershortdesc` processing instruction during preprocessing. These omissions have been corrected to aid in debugging. \(This change is relevant only within preprocessing, as these processing instructions are deleted when preprocessing completes.\) [\#4155](https://github.com/dita-ot/dita-ot/issues/4155)
-   When building HTML output, earlier versions reported XSLT errors while resolving custom header files if paths used Windows backslash characters “`\`” as separators. Path separators in **args.ftr**, **args.hdf**, and **args.hdr** parameter values are now converted to the forward slash character “`/`” to ensure URLs are valid before they are passed to XSLT. [\#4218](https://github.com/dita-ot/dita-ot/issues/4218), [\#4226](https://github.com/dita-ot/dita-ot/issues/4226)
-   For cross-references to a topic, the target topic’s short description is processed to create a link description. When that `<shortdesc>` element contained another cross-reference, earlier versions did not process it correctly, and reported DOTX031E \(file not available\) errors during processing. This issue is now fixed, and link descriptions are created correctly. [\#4221](https://github.com/dita-ot/dita-ot/issues/4221), [\#4239](https://github.com/dita-ot/dita-ot/issues/4239)
-   Build scripts have been updated to ensure unit tests run correctly during Gradle builds. [\#4230](https://github.com/dita-ot/dita-ot/issues/4230)
-   The RELAX NG grammar caching changes in DITA-OT 4.0 introduced a configuration bug that accidentally disabled XML Schema Definition validation. Processing and tests have been updated to ensure that XSD-based maps and topic files can be published correctly. [\#3926](https://github.com/dita-ot/dita-ot/issues/3926), [\#4234](https://github.com/dita-ot/dita-ot/issues/4234), [\#4238](https://github.com/dita-ot/dita-ot/issues/4238)
-   When logging was changed to use processing mode in DITA-OT 4.1, the change logged the exception without location. Logging code has been corrected to restore the location information to the exception, so errors once again show the line/column number where the problem appears. [\#4187](https://github.com/dita-ot/dita-ot/issues/4187), [\#4240](https://github.com/dita-ot/dita-ot/issues/4240), [\#4248](https://github.com/dita-ot/dita-ot/issues/4248)
-   Several dependencies have been upgraded to include the latest utility versions and fix security issues in bundled libraries:
    -   Guava 32.1.1 [\#4227](https://github.com/dita-ot/dita-ot/issues/4227), [\#4245](https://github.com/dita-ot/dita-ot/issues/4245)
    -   Jackson 2.15.2 [\#4216](https://github.com/dita-ot/dita-ot/issues/4216), [\#4228](https://github.com/dita-ot/dita-ot/issues/4228)
    -   Logback 1.4.8 and SLF4J 2.0.7 [\#4246](https://github.com/dita-ot/dita-ot/issues/4246), [\#4250](https://github.com/dita-ot/dita-ot/issues/4250)
    -   Saxon 12.3 [\#4241](https://github.com/dita-ot/dita-ot/issues/4241), [\#4247](https://github.com/dita-ot/dita-ot/issues/4247), [\#4250](https://github.com/dita-ot/dita-ot/issues/4250)

For additional information on the issues resolved since the previous release, see the [4.1.1 milestone](https://github.com/dita-ot/dita-ot/issues?q=milestone%3A4.1.1+is%3Aclosed) and [changelog](https://github.com/dita-ot/dita-ot/compare/4.1...4.1.1) on GitHub.

## DITA-OT 4.1 released June 22, 2023

DITA Open Toolkit Release 4.1 includes a new version of the Lightweight DITA plug-in with significant enhancements to Markdown processing, and updates for the latest DITA 2.0 draft standard.

### Plug-in development features

-   Since DITA-OT 3.5, the `dita` **plugins** subcommand shows a list of the currently installed plug-ins by plug-in ID. To make it easier to determine which version of each plug-in is installed, the output now includes the version number for each plug-in as specified in the `plugin.xml` file. [\#4137](https://github.com/dita-ot/dita-ot/issues/4137), [\#4141](https://github.com/dita-ot/dita-ot/issues/4141)
-   Previously only files referenced from the start map could be parsed using a custom parser. The start map itself was always processed as DITA XML. As of DITA-OT 4.1, processing has been updated to also allow the start map to use a custom parser. This change allows recent versions of the LwDITA plug-in to process Markdown maps. [\#4159](https://github.com/dita-ot/dita-ot/issues/4159)
-   Plug-in developers can now configure custom parsers via SAX properties that provide a list of formats and processing mode. The LwDITA plug-in uses this mechanism to configure the options supported for Markdown and MDITA. [\#4205](https://github.com/dita-ot/dita-ot/issues/4205)

### Lightweight DITA and Markdown updates

The `org.lwdita` plug-in has been updated to version 5.5, which includes performance improvements and updates to Markdown processing to reflect recent changes to the latest LwDITA drafts from OASIS.

-   **Markdown output**

    -   When generating Markdown output, the less-than “&lt;” and greater-than “&gt;” characters are now added to `<xmlelement>` content as in HTML and PDF output.
    -   Markdown output now treats programming and software domain elements as code spans and wraps the content in backtick quotes \(```\) for better correspondence with HTML5 output, which wraps these elements in `<code>`.
-   **Markdown input**

    -   Standard Markdown syntax can now be used to indicate a span of code by wrapping it with backtick quotes \(```\). In Markdown DITA input, these constructs are converted to DITA `<codeph>` elements on import, and rendered as `<code>` elements in HTML output. In MDITA input, backtick code spans are parsed as teletype `<tt>` elements to align with LwDITA, which supports teletype highlighting in XDITA.
    -   The LwDITA plug-in supports a new `$schema` key in the YAML front matter block. This key can be used to define parsing options in topic files for more control over how Markdown content is converted to DITA. For more information, see [Markdown schemas](../reference/markdown/Markdown-schemas.md).
    -   Earlier versions of the plug-in failed to parse certain Markdown tables correctly. Table parsing has been improved to ensure these cases are properly processed.
    -   The MDITA core profile can now be specified via the new schema key in the YAML front matter block.
    -   Any `linefeed` processing instructions in Markdown input are now converted to line feeds in HTML5 and PDF output.
    -   Markdown DITA supports both loose and [tight](https://spec.commonmark.org/0.30/#tight) list spacing \(with no blank lines between list items\). MDITA treats all lists as loose, and wraps each list item in a paragraph: `<li><p>item</p></li>`.
    -   DITA maps can now be written in Markdown using standard Markdown syntax for links and lists.
        -   In Markdown DITA, the schema key in the YAML front matter block is used to define the file as a map. Unordered list items create `<topicref>` elements, and ordered list items create `<topicref>` elements with `@collection-type`=sequence. List items without a link are treated as topic heads.
        -   In MDITA, maps use the file name extension `mditamap` to define the file as a map. Both ordered and unordered list items create `<topicref>`, and any unlinked topic heads are ignored.
-   The flexmark Markdown parsing library has been updated to version 0.64.

-   The XDITA plug-in has been updated to version 0.3.0, which includes recent changes to the grammar files from OASIS \(as of June 18, 2023\). [\#4214](https://github.com/dita-ot/dita-ot/issues/4214)


### Updated DITA 2.0 preview

In addition to the [DITA 2.0 preview support](../reference/dita-v2-0-support.md) provided in DITA-OT 3.5 – 4.0, this release includes updated processing for the latest draft versions of the DITA 2.0 grammar files from OASIS \(as of April 26, 2023\).

-   DITA 2.0 splits the programming and syntax domains \(so you can use one without the other\).

    The syntax diagram elements move from the programming domain to a new syntax diagram domain, which results in new class attribute tokens. All elements and content models remain the same.

    HTML5 and PDF processing has been updated for DITA-OT 4.1 to support syntax diagram elements from DITA 2.0, so that processing matches what those elements did in DITA 1.3. [\#4082](https://github.com/dita-ot/dita-ot/issues/4082)

-   DITA 2.0 removes the xNAL domain and classification domains. [\#4177](https://github.com/dita-ot/dita-ot/issues/4177)

DITA documents that reference the draft grammar files can be parsed, and where features overlap with DITA 1.3, those features will work as expected.

**Note:** Other new or revised features proposed for DITA 2.0 are not yet supported. Additional features will be implemented in future versions of DITA-OT as the specification evolves.

### Enhancements and changes

DITA Open Toolkit Release 4.1 includes the following enhancements and changes to existing features:

-   When publishing to HTML and PDF, email links no longer include the `mailto:` prefix in the default link text. [\#4020](https://github.com/dita-ot/dita-ot/issues/4020), [\#4089](https://github.com/dita-ot/dita-ot/issues/4089)
-   When filtering profiled content with DITAVAL files that exclude content by default, the DOTJ031I message no longer appears when no rule is specified for a certain attribute. [\#4048](https://github.com/dita-ot/dita-ot/issues/4048), [\#4073](https://github.com/dita-ot/dita-ot/issues/4073)
-   The Java code has been refactored to use new language and library features from recent Java versions. These changes make the code more future-proof and easier to maintain. [\#4090](https://github.com/dita-ot/dita-ot/issues/4090), [\#4091](https://github.com/dita-ot/dita-ot/issues/4091), [\#4092](https://github.com/dita-ot/dita-ot/issues/4092), [\#4121](https://github.com/dita-ot/dita-ot/issues/4121)
-   The following bundled plug-ins have been upgraded to the latest versions:
    -   The Normalized DITA plug-in version 1.1 now removes unnecessary key artefacts like `@keys`, `@keyref` or `<keydef>` after key resolution, and `<ditavalref>` elements after branch filter resolution. [\#4140](https://github.com/dita-ot/dita-ot/issues/4140)
    -   The Lightweight DITA plug-in version 5.5 includes the [Lightweight DITA and Markdown updates](index.md#lwdita) described above. [\#4167](https://github.com/dita-ot/dita-ot/issues/4167), [\#4178](https://github.com/dita-ot/dita-ot/issues/4178), [\#4210](https://github.com/dita-ot/dita-ot/issues/4210)
    -   The PDF Theme plug-in version 0.7.0 adds support for tasks, and the hazard, highlight, markup, UI, and XML domains, so you can now style these elements in a YAML theme file without building a custom PDF plug-in. [\#4194](https://github.com/dita-ot/dita-ot/issues/4194)
-   Several bundled dependencies have been upgraded to the latest versions:
    -   Ant 1.10.13 [\#4182](https://github.com/dita-ot/dita-ot/issues/4182)
    -   FOP 2.8 [\#4183](https://github.com/dita-ot/dita-ot/issues/4183), [\#4011](https://github.com/dita-ot/dita-ot/issues/4011)
    -   Gradle wrapper 7.6.1 [\#4197](https://github.com/dita-ot/dita-ot/issues/4197)
    -   Saxon 12.2 [\#4130](https://github.com/dita-ot/dita-ot/issues/4130)

### Bug fixes

DITA Open Toolkit Release 4.1 provides fixes for the following bugs:

-   Earlier versions of [Map-first preprocessing](../reference/map-first-preprocessing.md) \(preprocess2\) failed to copy non-DITA files to the output directory. Processing has been updated to copy media files and other linked assets. [\#3242](https://github.com/dita-ot/dita-ot/issues/3242), [\#3966](https://github.com/dita-ot/dita-ot/issues/3966), [\#4132](https://github.com/dita-ot/dita-ot/issues/4132)
-   When a map contained references to nested subtopics within the same topic file, earlier versions would process the file multiple times during branch filtering. The output was correct but runtime was increased. This issue has been fixed so that the topic file is only filtered once. [\#3903](https://github.com/dita-ot/dita-ot/issues/3903), [\#4152](https://github.com/dita-ot/dita-ot/issues/4152)
-   In earlier versions, cross-references to `<fn>` footnote elements without target text were rendered with two levels of `<sup>` superscript formatting in XHTML and HTML5 output. Now, these links are only superscripted once. [\#3967](https://github.com/dita-ot/dita-ot/issues/3967), [\#3968](https://github.com/dita-ot/dita-ot/issues/3968)
-   When generating PDF output, earlier versions failed with the PDFX005F error when topic references targeted external resources with the `@scope` attribute set to `external`. Processing has been updated to properly recognize external resources and allow builds to complete. [\#4131](https://github.com/dita-ot/dita-ot/issues/4131)
-   Earlier versions included DITA 2.0 grammar files from OASIS that referenced non-public URNs. The files have been updated to the latest versions \(as of April 26, 2023\), which include updated references in the RELAX NG files. [\#4144](https://github.com/dita-ot/dita-ot/issues/4144), [\#4177](https://github.com/dita-ot/dita-ot/issues/4177)
-   Earlier versions reported errors when processing DITA 2.0 content with empty `@specializations` attribute values. Processing has been updated to handle these cases correctly. [\#4165](https://github.com/dita-ot/dita-ot/issues/4165)
-   When generating HTMLHelp with DITA-OT 4.0, builds failed with the DOTA015F error. HTMLHelp has been updated to replace the outdated `preprocess.copy-image.skip` property with the corresponding DITA 4.0 `build-step.copy-image` property for compatibility with recent toolkit versions. [\#4181](https://github.com/dita-ot/dita-ot/issues/4181), [\#4186](https://github.com/dita-ot/dita-ot/issues/4186)
-   When topic short descriptions contain cross-reference links that point to one another in circular references across topics, earlier versions would fail with an infinite-recursion stylesheet loop. Now, `<shortdesc>` descriptions in referenced elements are processed only one level deep. [\#4184](https://github.com/dita-ot/dita-ot/issues/4184), [\#4185](https://github.com/dita-ot/dita-ot/issues/4185)
-   In earlier versions, setting the **processing-mode** parameter to strict would only stop processing if errors were reported from the Java code. Any XSLT errors were logged to the console, but processing continued. Now, XSLT errors will also stop processing, so strict mode is a bit … *stricter*. [\#4187](https://github.com/dita-ot/dita-ot/issues/4187)

### Contributors

DITA Open Toolkit Release 4.1 includes [code contributions](https://github.com/dita-ot/dita-ot/graphs/contributors) by the following people:

1.  Jarno Elovirta
2.  Robert D Anderson
3.  Radu Coravu
4.  Chris Papademetrious
5.  Roger Sheen
6.  Duna Marius Cosmin
7.  Josh Johnson
8.  Toshihiko Makita

For the complete list of changes since the previous release, see the [changelog](https://github.com/dita-ot/dita-ot/compare/4.0...4.1) on GitHub.

### Documentation updates

The documentation for DITA Open Toolkit Release 4.1 provides corrections and improvements to existing topics, along with new information in the following topics:

-   [Publishing with project files](../topics/using-project-files.md)
-   [Markdown input](../topics/markdown-input.md)
-   [Generating Markdown output](../topics/dita2markdown.md)
-   [Extension point reference](../extension-points/plugin-extension-points.md)
-   [Markdown formats](../reference/markdown-formats.md)
    -   [Markdown DITA syntax](../reference/markdown/Markdown-DITA-syntax.md)
    -   [MDITA syntax](../reference/markdown/MDITA-syntax.md)
    -   [Format comparison](../reference/markdown/Format-comparison.md)
    -   [Markdown schemas](../reference/markdown/Markdown-schemas.md)
    -   [Custom schemas](../reference/markdown/Custom-schemas.md)

For additional information on documentation issues resolved in DITA Open Toolkit Release 4.1, see the [4.1 milestone](https://github.com/dita-ot/docs/issues?q=milestone%3A4.1+is%3Aclosed) in the documentation repository.

DITA Open Toolkit Release 4.1 includes [documentation contributions](https://github.com/dita-ot/docs/graphs/contributors) by the following people:

1.  Roger Sheen
2.  Jarno Elovirta
3.  Lief Erickson
4.  Darrenn Jackson
5.  Mark Giffin

For the complete list of documentation changes since the previous release, see the [changelog](https://github.com/dita-ot/docs/compare/4.0...4.1).

