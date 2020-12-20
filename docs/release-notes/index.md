# DITA Open Toolkit 3.6 Release Notes

DITA Open Toolkit 3.6 includes performance enhancements such as processing in parallel and in memory, support for PDF changebars with Apache™ FOP, and an updated preview of features for the latest draft of the upcoming DITA 2.0 standard, including the `audio` and `video` elements, and the new emphasis domain.

DITA-OT releases follow [semantic versioning](https://semver.org) guidelines. Version numbers use the `major.minor.patch` syntax, where major versions may include incompatible API changes, minor versions add functionality in a backwards-compatible manner and patch versions are maintenance releases that include backwards-compatible bug fixes.

**Tip:** Download the dita-ot-3.6.zip package from the project website at [dita-ot.org/download](https://www.dita-ot.org/download).

## Requirements

DITA-OT is designed to run on Java version 8u101 or later and built and tested with the Open Java Development Kit \(OpenJDK\). Compatible Java distributions are available from multiple sources:

-   You can download the Oracle JRE or JDK from [oracle.com/technetwork/java](http://www.oracle.com/technetwork/java/javase/downloads) under commercial license.
-   OpenJDK is a free open-source implementation of Java available from [adoptopenjdk.net](https://adoptopenjdk.net).
-   Free OpenJDK distributions are also available from other vendors, including [Amazon Corretto](https://aws.amazon.com/corretto/), [Azul Zulu](https://www.azul.com/downloads/zulu/), and [Red Hat](https://developers.redhat.com/products/openjdk/download).

## DITA-OT 3.6 released December 19, 2020

DITA Open Toolkit Release 3.6 includes performance enhancements such as processing in parallel and in memory, support for PDF changebars with Apache FOP, and an updated preview of features for the latest draft of the upcoming DITA 2.0 standard, including the `audio` and `video` elements, and the new emphasis domain.

### Parallel processing

Preprocessing module code can now be run in parallel by setting the parallel parameter to true. The performance benefits this option provides depend heavily on the source file set, the DITA features used in the project, and the computer doing the processing, but under the right circumstances, you may see notable improvements when this option is enabled.

### In-memory processing

DITA-OT 3.6 introduces a new Store API with preview support for in-memory processing. The Cache Store can be activated by setting the store-type parameter to memory. In-memory processing provides performance advantages in I/O bound environments such as cloud computing platforms, where processing time depends primarily on how long it takes to read and write temporary files. For more information, see [Store API – Processing in memory](../reference/store-api.md).

### Additional performance improvements

DITA-OT 3.6 includes a series of related changes designed to improve the performance of DITA transformations.

-   A new --repeat option can be passed to the dita command to run the process a certain number of times. This option can be used by plug-in developers to measure performance. \(Timings for the first transformation are often dominated by Java warm-up time.\) [\#3616](https://github.com/dita-ot/dita-ot/issues/3616)

    To run a conversion five times, for example, use --repeat=5. The duration of each execution will appear in the console when the final transformation is complete.

    ```
    $ dita --input=docsrc/samples/sequence.ditamap --format=html5 --repeat=5
    1 11281ms
    2 4132ms
    3 3690ms
    4 4337ms
    5 3634ms
    ```

-   The DITA-OT Java code uses a new caching `DitaClass.getInstance(cls)` factory method rather than generating `DitaClass` instances directly. This allows previously created instances to be re-used, which reduces the number of instances that need to be created. [\#3569](https://github.com/dita-ot/dita-ot/issues/3569)
-   The Java code for several preprocessing modules has been refactored to use concurrent sets or queues. This helps to speed up certain operations during preprocessing, allowing builds to complete faster. [\#3570](https://github.com/dita-ot/dita-ot/issues/3570)
-   The Java code now uses a `BufferedWriter` to serialize `Job` objects, which significantly improves UTF-8 encoding performance when writing the .job.xml file. [\#3583](https://github.com/dita-ot/dita-ot/issues/3583)

### PDF changebars with Apache FOP

For DITA-OT 3.4, the bundled Apache™ Formatting Objects Processor library was upgraded to version 2.4, which included support for changebars, but those features were not yet enabled in DITA-OT 3.4 pending further testing. DITA-OT 3.6 removes the FOP-specific overrides that disabled changebars in earlier versions, allowing the default PDF2 flagging routines to be applied when generating PDFs with FOP. For details, see [Generating revision bars](../topics/pdf2-creating-change-bars.md).

Plug-ins that implemented custom FOP flagging by overriding the org.dita.pdf2.fop/xsl/fo/flagging\_fop.xsl stylesheet in prior versions will need to be updated, as this file is no longer available in DITA-OT 3.6. [\#3511](https://github.com/dita-ot/dita-ot/issues/3511), [\#3591](https://github.com/dita-ot/dita-ot/issues/3591)

### Updated DITA 2.0 preview

In addition to the [DITA 2.0 preview support](../reference/dita-v2-0-support.md) provided in DITA-OT 3.5, this release includes updated processing support for the latest DRAFT versions of the DITA 2.0 DTD and RELAX NG grammar files from OASIS \(as of October 2020\). [\#3586](https://github.com/dita-ot/dita-ot/issues/3586), [\#3601](https://github.com/dita-ot/dita-ot/issues/3601), [\#3617](https://github.com/dita-ot/dita-ot/issues/3617), [\#3652](https://github.com/dita-ot/dita-ot/issues/3652)

-   Where earlier DITA versions relied on the `object` to embed media in DITA source files, DITA 2.0 provides new `audio` and `video` elements that correspond to their HTML5 equivalents.
-   For HTML5 compatibility, the new emphasis domain adds support for the `strong` and `em` elements in addition to the existing `b` and `i` elements in the highlighting domain.
-   The troubleshooting domain has been updated with additional constructs that can be used to provide detailed diagnostic information.
-   Several obsolete elements and attributes have been removed from DITA 2.0, including:
    -   `boolean`
    -   `data-about`
    -   `indextermref`
    -   `@alt` on `image`
    -   `@navtitle` on `topicref`
    -   `@query` on `topicref`
    -   `@refcols` on `simpletable`
    -   `@xtrc`
    -   `@xtrf`

DITA documents that reference the draft grammar files can be parsed, and where features overlap with DITA 1.3, those features will work as expected.

**Note:** Other new or revised features proposed for DITA 2.0 are not yet supported. Additional features will be implemented in future versions of DITA-OT as the specification evolves.

### Enhancements and changes

DITA Open Toolkit Release 3.6 includes the following enhancements and changes to existing features:

-   The `@rotate` attribute on table `entry` elements is now respected when generating HTML5 output. The rotation is implemented by setting the CSS `writing-mode` property to `vertical-rl` to rotate the cell content. This property is rendered correctly in Mozilla Firefox, but unevenly supported by other browsers. The `rotate` class is passed to HTML5 output, so custom plug-ins can implement alternative presentation rules in CSS if necessary. [\#3448](https://github.com/dita-ot/dita-ot/issues/3448), [\#3541](https://github.com/dita-ot/dita-ot/issues/3541), [\#3651](https://github.com/dita-ot/dita-ot/issues/3651)
-   User-facing text for the dita command line interface has been extracted to a strings file to facilitate editing. The cli\_en\_US.properties is provided in the resources folder as a basis for customization and localization. [\#3495](https://github.com/dita-ot/dita-ot/issues/3495), [\#3523](https://github.com/dita-ot/dita-ot/issues/3523)
-   The new `Store` implementation that supports in-memory processing includes an immutable document reader method that can be used to request a document that doesn't need to change during processing. This approach facilitates caching and helps to speed up processing. [\#3506](https://github.com/dita-ot/dita-ot/issues/3506), [\#3548](https://github.com/dita-ot/dita-ot/issues/3548)
-   In earlier versions, variations in reference capitalization could cause unexpected results when building output on case-sensitive file systems. DITA-OT now warns when file references use incorrect case. \(For example, if maps reference Topic.dita, but the filename on disk is actually topic.dita.\) In strict processing mode, this is considered a fatal error; in lax processing mode, the file reference is rewritten to use the same case as the file system. [\#3535](https://github.com/dita-ot/dita-ot/issues/3535)
-   The --filter option can now be passed to the dita multiple times in a single command-line invocation to apply conditions from several DITAVAL files at once. [\#3556](https://github.com/dita-ot/dita-ot/issues/3556)
-   The bundled Apache Formatting Objects Processor \(FOP\) has been upgraded to version 2.5, which includes security updates to various embedded libraries. [\#3558](https://github.com/dita-ot/dita-ot/issues/3558), [\#3630](https://github.com/dita-ot/dita-ot/issues/3630)
-   The deprecated `msgprefix` XSL variable \(“DOTX”\) has been removed. This variable was originally deprecated in DITA-OT 2.3, but still defined in several stylesheets. Importing the common XSL module output-message.xsl no longer requires this variable to be defined. [\#3562](https://github.com/dita-ot/dita-ot/issues/3562)
-   The S9api message listener from the Saxon API is now used to forward log messages to the `DITAOTLogger`. This allows message levels and error codes to be passed from XSLT to Java code for improved debugging. [\#3564](https://github.com/dita-ot/dita-ot/issues/3564)
-   HTML5 output now includes additional metadata to indicate that the content was produced using DITA Open Toolkit. [\#3594](https://github.com/dita-ot/dita-ot/issues/3594)

    ```language-html
    <meta name="generator" content="DITA-OT"/>
    ```

-   Up to version 3.5, DITA-OT included the [Dublin Core Metadata Element Set](https://dublincore.org/specifications/dublin-core/dcmi-terms) in both XHTML and HTML5 output. For DITA-OT 3.6, this capability was extracted to a separate plugin, and Dublin Core metadata is no longer generated in the default HTML5 output. [\#3595](https://github.com/dita-ot/dita-ot/issues/3595)

    If necessary, the [org.dita.html5.dublin-core](https://github.com/dita-ot/org.dita.html5.dublin-core/) plug-in can be installed from the plug-in registry at [dita-ot.org/plugins](https://www.dita-ot.org/plugins) to add Dublin Core metadata to HTML5. To install the plug-in, run the following command:

    ```syntax-bash
    dita install org.dita.html5.dublin-core
    ```

-   In XHTML output, previous versions failed to distinguish *Notice* note types from regular notes, prefixing both with **Note**. Support has been backported from HTML5 to XHTML to prefix notices with **Notice** as expected. [\#3599](https://github.com/dita-ot/dita-ot/issues/3599), [\#3600](https://github.com/dita-ot/dita-ot/issues/3600)
-   Unused code for flagging and key processing has been removed along with related files that have been deprecated since version 2.1, including the base flag.xsl stylesheet, the generated keydef.xml file, and schemekeydef.xml. [\#3602](https://github.com/dita-ot/dita-ot/issues/3602), [\#3603](https://github.com/dita-ot/dita-ot/issues/3603)
-   Remaining inline style attributes were removed from HTML5 code, which prevented custom plug-ins from overriding the presentation of the corresponding elements, including:

    -   `line-through` and `overline` elements
    -   syntax diagrams
    -   long quote citations
    -   Boolean states
    These changes move the default presentation rules to CSS to allow users to override these styles in custom stylesheets. The output is visually equivalent to the results generated by previous toolkit versions. [\#3632](https://github.com/dita-ot/dita-ot/issues/3632)

    **Important:** In publishing environments that do not use the default common CSS files, these styles may need to be implemented in custom stylesheets.


### Bugs

DITA Open Toolkit Release 3.6 provides fixes for the following bugs:

-   Folder names in development build archives previously included the “`+`” plus sign, which caused errors when running from the unpacked directory. The snapshot folder name syntax has been updated to use the “`@`” at sign instead, which allows builds to run directly from the extracted folder. [\#2414](https://github.com/dita-ot/dita-ot/issues/2414), [\#3623](https://github.com/dita-ot/dita-ot/issues/3623)

-   The license text for the beta DITA 2.0 grammar file plug-in was missing in DITA-OT 3.5 and is now included in the distribution package. [\#3608](https://github.com/dita-ot/dita-ot/issues/3608), [\#3649](https://github.com/dita-ot/dita-ot/issues/3649)

-   The Java code has been refactored to anticipate cases where resources are missing or incorrectly defined.
    -   The `File.toURI()` method has been updated to ensure that the generated URI for a directory will always end in a trailing slash. This prevents unexpected errors in cases when the `File` input points to a path that doesn’t exist. [\#3621](https://github.com/dita-ot/dita-ot/issues/3621), [\#3624](https://github.com/dita-ot/dita-ot/issues/3624), [\#3626](https://github.com/dita-ot/dita-ot/issues/3626)
    -   The `JobSourceSet` has been fixed to handle cases where the `src` input is `null`. [\#3625](https://github.com/dita-ot/dita-ot/issues/3625)
-   In DITA-OT 3.5.4, the HTMLHelp stylesheet map2hhcImpl.xsl included an invalid code remnant left over from previous edits. The unnecessary line has been removed. [\#3627](https://github.com/dita-ot/dita-ot/issues/3627), [\#3634](https://github.com/dita-ot/dita-ot/issues/3634)

### Contributors

DITA Open Toolkit Release 3.6 includes [code contributions](https://github.com/dita-ot/dita-ot/graphs/contributors) by the following people:

1.  Jarno Elovirta
2.  Roger Sheen
3.  Robert D Anderson
4.  Radu Coravu
5.  David Bertalan

For the complete list of changes since the previous release, see the [changelog](https://github.com/dita-ot/dita-ot/compare/3.5...3.6) on GitHub.

### Documentation updates

The documentation for DITA Open Toolkit Release 3.6 provides corrections and improvements to existing topics, along with new information in the following topics:

-   [Store API – Processing in memory](../reference/store-api.md)
-   [DITA 2.0 preview support](../reference/dita-v2-0-support.md)
-   [Migrating to release 3.6](../topics/migrating-to-3.6.md)
-   [Speeding up builds](../topics/reducing-processing-time.md)
-   [Common parameters](../parameters/parameters-base.md)
-   [Using the dita command](../topics/build-using-dita-command.md)
-   [Arguments and options for the dita command](../parameters/dita-command-arguments.md)

For additional information on documentation issues resolved in DITA Open Toolkit Release 3.6, see the [3.6 milestone](https://github.com/dita-ot/docs/issues?q=milestone%3A3.6+is%3Aclosed) in the documentation repository.

DITA Open Toolkit Release 3.6 includes [documentation contributions](https://github.com/dita-ot/docs/graphs/contributors) by the following people:

1.  Roger Sheen
2.  Jarno Elovirta
3.  Lief Erickson
4.  Heston Hoffman

For the complete list of documentation changes since the previous release, see the [changelog](https://github.com/dita-ot/docs/compare/3.5...3.6).

