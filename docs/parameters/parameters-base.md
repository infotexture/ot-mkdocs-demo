# Common parameters

Certain parameters apply to all transformations that DITA Open Toolkit supports.

-   **__args.debug__**

    Specifies whether debugging information is included in the log. The allowed values are yes and no; the default value is no.

-   **__args.draft__**

    Specifies whether the content of &lt;draft-comment&gt; and &lt;required-cleanup&gt; elements is included in the output. The allowed values are yes and no; the default value is no.

    Corresponds to the XSLT parameter **DRAFT** in most XSLT modules.

    **Tip:** For PDF output, setting the **args.draft** parameter to yes causes the contents of the `<titlealts>` element to be rendered below the title.

-   **__args.figurelink.style__**

    Specifies how cross references to figures are styled in output. The allowed values are NUMBER, TITLE, and NUMTITLE.

    Specifying NUMBER results in "Figure 5"; specifying TITLE results in the title of the figure. Corresponds to the XSLT parameter **FIGURELINK**.

    **Note:** Support for PDF was added in DITA-OT 2.0. By default PDF uses the value NUMTITLE, which is not supported for other transformation types; this results in "Figure 5. Title".

-   **__args.filter__**

    Specifies filter file\(s\) used to include, exclude, or flag content. Relative paths are resolved against the DITA-OT base directory \(for backwards compatibility\) and internally converted to absolute paths.

    **Note:**

    To specify multiple filter files, use the system path separator character to delimit individual file paths \(semicolon ‘`;`’ on Windows, and colon ‘`:`’ on macOS and Linux\) and wrap the value in quotes:

    `--args.filter="filter1.ditaval;filter2.ditaval;filter3.ditaval"`

    DITAVAL files are evaluated in the order specified, so conditions specified in the first file take precedence over matching conditions specified in later files, just as conditions at the start of a DITAVAL document take precedence over matching conditions later in the same document.

-   **__args.gen.task.lbl__**

    Specifies whether to generate headings for sections within task topics. The allowed values are YES and NO.

    Corresponds to the XSLT parameter **GENERATE-TASK-LABELS**.

-   **__args.grammar.cache__**

    Specifies whether the grammar-caching feature of the XML parser is used. The allowed values are yes and no; the default value is yes.

    **Note:** This option dramatically speeds up processing time. However, there is a known problem with using this feature for documents that use XML entities. If your build fails with parser errors about entity resolution, set this parameter to no.

-   **__args.input__**

    Specifies the main file for your documentation project.

    This parameter corresponds to the command-line argument [--input](dita-command-arguments.md#input).

    Typically this is a DITA map, however it also can be a DITA topic if you want to transform a single DITA file. The path can be absolute, relative to **args.input.dir**, or relative to the current directory if **args.input.dir** is not defined.

-   **__args.input.dir__**

    Specifies the base directory for your documentation project.

-   **__args.output.base__**

    Specifies the name of the output file without file extension.

-   **__args.rellinks__**

    Specifies which links to include in the output. The following values are supported:

    -   none – No links are included.
    -   all – All links are included.
    -   noparent – Ancestor and parent links are not included.
    -   nofamily – Parent, ancestor, child, descendant, sibling, next, previous, and cousin links are not included.
    For PDF output, the default value is nofamily. Other formats include all link roles except `ancestor` links.

-   **__args.resources__**

    Specifies resource files.

    This parameter corresponds to the command-line option [--resource](dita-command-arguments.md#resource).

    Resource files can be used to convert partial documentation sets by processing input with additional information.

    For example, to process a single topic file with a map that contains key definitions, use a command like this:

    ```syntax-bash
    `dita` **--input**=`topic.dita` **--format**=html5 **--args.resources**=`keys.ditamap`
    ```

    To convert a chapter map to HTML5 and insert related links from relationship tables in a separate map, use:

    ```syntax-bash
    `dita` **--input**=`chapter.ditamap` **--format**=html5 **--args.resources**=`reltables.ditamap`
    ```

-   **__args.tablelink.style__**

    Specifies how cross references to tables are styled. The allowed values are NUMBER, TITLE, and NUMTITLE.

    Specifying NUMBER results in "Table 5"; specifying TITLE results in the title of the table. Corresponds to the XSLT parameter **TABLELINK**.

    **Note:** Support for PDF was added in DITA-OT 2.0. By default PDF uses the value NUMTITLE, which is not supported for other transformation types; this results in "Table 5. Title".

-   **__build-step.branch-filter__**

    Run process branch-filter The allowed values are true and false; the default value is true.

-   **__build-step.chunk__**

    Run process chunk The allowed values are true and false; the default value is true.

-   **__build-step.clean-preprocess__**

    Run process clean-preprocess The allowed values are true and false; the default value is true.

-   **__build-step.clean-temp__**

    Run process clean-temp The allowed values are true and false; the default value is true.

-   **__build-step.coderef__**

    Run process coderef The allowed values are true and false; the default value is true.

-   **__build-step.conref__**

    Run process conref The allowed values are true and false; the default value is true.

-   **__build-step.copy-flag__**

    Run process copy-flag The allowed values are true and false; the default value is true.

-   **__build-step.copy-html__**

    Run process copy-html The allowed values are true and false; the default value is true.

-   **__build-step.copy-image__**

    Run process copy-image The allowed values are true and false; the default value is true.

-   **__build-step.keyref__**

    Run process keyref The allowed values are true and false; the default value is true.

-   **__build-step.map-profile__**

    Run process map-profile The allowed values are true and false; the default value is true.

-   **__build-step.maplink__**

    Run process maplink The allowed values are true and false; the default value is true.

-   **__build-step.mapref__**

    Run process mapref The allowed values are true and false; the default value is true.

-   **__build-step.move-meta-entries__**

    Run process move-meta-entries The allowed values are true and false; the default value is true.

-   **__build-step.normalize-codeblock__**

    Run process normalize-codeblock The allowed values are true and false; the default value is true.

-   **__build-step.profile__**

    Run process profile The allowed values are true and false; the default value is false.

-   **__build-step.topic-profile__**

    Run process topic-profile The allowed values are true and false; the default value is false.

-   **__build-step.topicpull__**

    Run process topicpull The allowed values are true and false; the default value is true.

-   **__clean.temp__**

    Specifies whether DITA-OT deletes the files in the temporary directory after it finishes a build. The allowed values are yes and no; the default value is yes.

-   **__conserve-memory__**

    Conserve memory at the expense of processing speed. The allowed values are true and false; the default value is false.

-   **__default.language__**

    Specifies the language that is used if the input file does not have the `@xml:lang` attribute set on the root element. By default, this is set to en. The allowed values are those that are defined in IETF BCP 47, [Tags for Identifying Languages](https://tools.ietf.org/html/bcp47).

-   **__dita.dir__**

    Specifies where DITA-OT is installed.

-   **__dita.input.valfile__**

    Specifies a filter file to be used to include, exclude, or flag content.

    **Note:** This parameter is deprecated in favor of the **args.filter** parameter.

-   **__dita.temp.dir__**

    Specifies the location of the temporary directory.

    This parameter corresponds to the command-line option [--temp](dita-command-arguments.md#temp).

    The temporary directory is where DITA-OT writes intermediate files that are generated during the transformation process.

-   **__filter-stage__**

    Specifies whether filtering is done before all other processing, or after key and conref processing. The allowed values are early and late; the default value is early.

    **Note:** Changing the filtering stage may produce different results for the same initial data set and filtering conditions.

-   **__force-unique__**

    Generate copy-to attributes to duplicate topicref elements. The allowed values are true and false; the default value is false.

    Setting this to true ensures that unique output files are created for each instance of a resource when a map contains multiple references to a single topic.

-   **__generate-debug-attributes__**

    Specifies whether the @xtrf and @xtrc debugging attributes are generated in the temporary files. The following values are supported:

    -   true \(default\) – Enables generation of debugging attributes
    -   false – Disables generation of debugging attributes
    **Note:** Disabling debugging attributes reduces the size of temporary files and thus reduces memory consumption. However, the log messages no longer have the source information available and thus the ability to debug problems might deteriorate.

-   **__generate.copy.outer__**

    Adjust how output is generated for content that is located outside the directory containing the input resource \(DITA map or topic\). The following values are supported:

    -   1 \(default\) – Do not generate output for content that is located outside the DITA map directory.
    -   3 – Shift the output directory so that it contains all output for the publication.
    See [Handling content outside the map directory](generate-copy-outer.md) for more information.

-   **__link-crawl__**

    Specifies whether to crawl only those topic links found in maps, or all discovered topic links. The allowed values are map and topic; the default value is topic.

-   **__onlytopic.in.map__**

    Specifies whether files that are linked to, or referenced with a @conref attribute, generate output. The allowed values are true and false; the default value is false.

    If set to true, only files that are referenced directly from the map will generate output.

-   **__outer.control__**

    Specifies whether to warn or fail if content is located outside the directory containing the input resource \(DITA map or topic\). The following values are supported:

    -   fail – Fail quickly if files are going to be generated or copied outside of the directory.
    -   warn \(default\) – Complete the operation if files will be generated or copied outside of the directory, but log a warning.
    -   quiet – Quietly finish without generating warnings or errors.
    **Warning:** Microsoft HTML Help Compiler cannot produce HTML Help for documentation projects that use outer content. The content files must reside in or below the directory containing the root map file, and the map file cannot specify ".." at the start of the `@href` attributes for `<topicref>` elements.

-   **__output.dir__**

    Specifies the name and location of the output directory.

    This parameter corresponds to the command-line option [--output](dita-command-arguments.md#output).

    By default, the output is written to `*DITA-dir*/out`.

-   **__parallel__**

    Run processes in parallel when possible. The allowed values are true and false; the default value is false.

-   **__processing-mode__**

    Specifies how DITA-OT handles errors and error recovery. The following values are supported:

    -   strict – When an error is encountered, DITA-OT stops processing
    -   lax \(default\) – When an error is encountered, DITA-OT attempts to recover from it
    -   skip – When an error is encountered, DITA-OT continues processing but does not attempt error recovery
-   **__remove-broken-links__**

    Remove broken related links. The allowed values are true and false; the default value is false.

-   **__result.rewrite-rule.class__**

    Specifies the name of the Java class used to rewrite filenames.

    The custom class should implement the `org.dita.dost.module.RewriteRule` interface.

-   **__result.rewrite-rule.xsl__**

    Specifies the name of the XSLT file used to rewrite filenames.

    See [Adjusting file names in map-first pre-processing](../topics/plugin-rewrite-rules.md) for details.

-   **__root-chunk-override__**

    Override for map chunk attribute value.

    Acceptable values include any value normally allowed on the `@chunk` attribute. If the map does not have a `@chunk` attribute, this value will be used; if the map already has a `@chunk` attribute specified, this value will be used instead.

-   **__store-type__**

    Temporary file store type. The allowed values are file and memory; the default value is file.

    In-memory processing provides performance advantages in I/O bound environments such as cloud computing platforms, where processing time depends primarily on how long it takes to read and write temporary files. For more information, see [Store API – Processing in memory](../reference/store-api.md).

    **Important:** Custom plug-ins that expect to find certain files on disk in the temporary directory will not work with in-memory processing.

-   **__transtype__**

    Specifies the output format \(transformation type\).

    This parameter corresponds to the command-line argument [--format](dita-command-arguments.md#format).

    You can create plug-ins to add new output formats; by default, the following values are available:

    -   dita
    -   eclipsehelp
    -   html5
    -   htmlhelp
    -   markdown, markdown\_gitbook, and markdown\_github
    -   pdf
    -   xhtml
    **Tip:** See [DITA-OT transformations \(output formats\)](../topics/output-formats.md) for sample command line syntax and more information on each transformation.

-   **__validate__**

    Specifies whether DITA-OT validates the content. The allowed values are true and false; the default value is true.


**Related information**  


[Eclipse help transformation](../topics/dita2eclipsehelp.md)

[HTML help transformation](../topics/dita2htmlhelp.md)

[PDF transformation](../topics/dita2pdf.md)

[XHTML transformation](../topics/dita2xhtml.md)

[Setting parameters for custom HTML](../topics/html-customization-parameters.md)

[HTML5 transformation](../topics/dita2html5.md)

[Generating Markdown output](../topics/dita2markdown.md)

[Normalized DITA transformations](../topics/dita2dita.md)

