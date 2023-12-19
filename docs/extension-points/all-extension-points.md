# All DITA-OT extension points

The pre-defined extension points can be used to add new functionality to DITA-OT. If your toolkit installation includes custom plug-ins that define additional extension points, you can add to this list by rebuilding the DITA-OT documentation.

-   **__dita.conductor.target__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Adds an Ant import to the main Ant build file.

    **Attention:** This extension point is deprecated; use `ant.import` instead.

-   **__dita.conductor.target.relative__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Adds an Ant import to the main Ant build file.

    **Tip:** As of DITA-OT 3.0, the `ant.import` extension point can be used instead.

-   **__dita.conductor.plugin__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Ant conductor plug-in information

-   **__ant.import__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Adds an Ant import to the main Ant build file.

-   **__depend.preprocess.chunk.pre__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `chunk` step in the pre-processing stage.

-   **__depend.preprocess.clean-temp.pre__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `clean-temp` step in the pre-processing stage.

-   **__depend.preprocess.coderef.pre__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `coderef` step in the pre-processing stage.

-   **__org.dita.pdf2.catalog.relative__**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    Adds the content of a catalog file to the main catalog file for the PDF plug-in.

-   **__dita.xsl.conref__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Content reference XSLT import

-   **__dita.preprocess.conref.param__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Content reference XSLT parameters

-   **__depend.preprocess.conref.pre__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `conref` step in the pre-processing stage.

-   **__depend.preprocess.conrefpush.pre__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `conrefpush` step in the pre-processing stage.

-   **__depend.preprocess.copy-html.pre__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `copy-html` step in the pre-processing stage.

-   **__depend.preprocess.copy-files.pre__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `copy-files` step in the pre-processing stage.

-   **__depend.preprocess.copy-flag.pre__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `copy-flag` step in the pre-processing stage.

-   **__depend.preprocess.copy-image.pre__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `copy-image` step in the pre-processing stage.

-   **__depend.preprocess.copy-subsidiary.pre__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `copy-subsidiary` step in the pre-processing stage.

-   **__dita.parser__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Custom DITA parser

-   **__depend.preprocess.debug-filter.pre__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `debug-filter` step in the pre-processing stage.

-   **__dita.preprocess.debug-filter.param__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Debug filter module parameters

-   **__dita.preprocess.map-reader.param__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Debug filter module parameters

-   **__dita.preprocess.topic-reader.param__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Debug filter module parameters

-   **__dita.xsl.messages__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Adds new diagnostic messages to DITA-OT.

-   **__dita.conductor.eclipse.toc.param__**

    Defined in plug-in [`org.dita.eclipsehelp`](extension-points-in-org.dita.eclipsehelp.md).

    Pass parameters to the XSLT step that generates the Eclipse Help table of contents \(TOC\).

-   **__dita.xsl.eclipse.toc__**

    Defined in plug-in [`org.dita.eclipsehelp`](extension-points-in-org.dita.eclipsehelp.md).

    Overrides the default XSLT step that generates the Eclipse Help table of contents \(TOC\).

-   **__dita.map.eclipse.index.pre__**

    Defined in plug-in [`org.dita.eclipsehelp`](extension-points-in-org.dita.eclipsehelp.md).

    Runs an Ant target before the Eclipse index extraction process.

-   **__dita.xsl.eclipse.plugin__**

    Defined in plug-in [`org.dita.eclipsehelp`](extension-points-in-org.dita.eclipsehelp.md).

    Overrides the default XSLT step that generates the `plugin.xml` file for Eclipse Help.

-   **__dita.basedir-resource-directory__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Flag to use basedir as resource directory

-   **__dita.conductor.pdf2.formatter.check__**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    Formatter check

-   **__depend.org.dita.pdf2.format.post__**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    Formatting post-target

-   **__depend.org.dita.pdf2.format.pre__**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    Formatting pre-target

-   **__depend.org.dita.pdf2.format__**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    Formatting target

-   **__depend.preprocess.gen-list.pre__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `gen-list` step in the pre-processing stage.

-   **__dita.xsl.strings__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Generated text

-   **__dita.xsl.htmlhelp.map2hhc__**

    Defined in plug-in [`org.dita.htmlhelp`](extension-points-in-org.dita.htmlhelp.md).

    Overrides the default XSLT step that generates the HTML Help contents \(`.hhc`\) file.

-   **__dita.xsl.htmlhelp.map2hhp__**

    Defined in plug-in [`org.dita.htmlhelp`](extension-points-in-org.dita.htmlhelp.md).

    Overrides the default XSLT step that generates the HTML Help project \(`.hhp`\) file.

-   **__dita.conductor.html.param__**

    Defined in plug-in [`org.dita.xhtml`](extension-points-in-org.dita.xhtml.md).

    Pass parameters to the HTML and HTML Help transformations.

-   **__dita.html.extensions__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    HTML file extension

-   **__dita.xsl.html.cover__**

    Defined in plug-in [`org.dita.xhtml`](extension-points-in-org.dita.xhtml.md).

    Overrides the default HTML cover page generation process.

-   **__dita.xsl.htmltoc__**

    Defined in plug-in [`org.dita.xhtml`](extension-points-in-org.dita.xhtml.md).

    Overrides the default XSLT step that generates the HTML table of contents \(TOC\).

-   **__dita.xsl.xhtml__**

    Defined in plug-in [`org.dita.xhtml`](extension-points-in-org.dita.xhtml.md).

    Overrides the default HTML or XHTML transformation, including HTML Help and Eclipse Help. The referenced file is integrated directly into the XSLT step that generates XHTML.

-   **__dita.conductor.xhtml.toc.param__**

    Defined in plug-in [`org.dita.xhtml`](extension-points-in-org.dita.xhtml.md).

    Pass parameters to the XSLT step that generates the XHTML table of contents \(TOC\).

-   **__dita.conductor.html5.toc.param__**

    Defined in plug-in [`org.dita.html5`](extension-points-in-org.dita.html5.md).

    Pass parameters to the XSLT step that generates the HTML5 table of contents \(TOC\).

-   **__dita.xsl.html5.cover__**

    Defined in plug-in [`org.dita.html5`](extension-points-in-org.dita.html5.md).

    Overrides the default HTML5 cover page generation process.

-   **__dita.xsl.html5.toc__**

    Defined in plug-in [`org.dita.html5`](extension-points-in-org.dita.html5.md).

    Overrides the default XSLT step that generates the HTML5 table of contents \(TOC\).

-   **__dita.xsl.html5__**

    Defined in plug-in [`org.dita.html5`](extension-points-in-org.dita.html5.md).

    Overrides the default HTML5 transformation. The referenced file is integrated directly into the XSLT step that generates HTML5.

-   **__dita.conductor.html5.param__**

    Defined in plug-in [`org.dita.html5`](extension-points-in-org.dita.html5.md).

    Pass parameters to the HTML5 transformation.

-   **__dita.image.extensions__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Image file extension

-   **__depend.org.dita.pdf2.index__**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    Indexing target

-   **__depend.org.dita.pdf2.init.pre__**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    Initialization pre-target

-   **__dita.conductor.lib.import__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Adds a Java library to the DITA-OT classpath.

-   **__depend.preprocess.keyref.pre__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `keyref` step in the pre-processing stage.

-   **__dita.xsl.maplink__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Map link XSLT import

-   **__depend.preprocess.maplink.pre__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `maplink` step in the pre-processing stage.

-   **__dita.preprocess.mappull.param__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Map pull XSLT parameters

-   **__dita.xsl.mappull__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Map pull XSLT import

-   **__depend.preprocess.mappull.pre__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `mappull` step in the pre-processing stage.

-   **__dita.xsl.mapref__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Map reference XSLT import

-   **__dita.preprocess.mapref.param__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Map reference XSLT parameters

-   **__depend.preprocess.mapref.pre__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `mapref` step in the pre-processing stage.

-   **__dita.xsl.markdown__**

    Defined in plug-in [`org.lwdita`](extension-points-in-org.lwdita.md).

    Markdown overrides XSLT import

-   **__depend.preprocess.move-meta-entries.pre__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `move-meta-entries` step in the pre-processing stage.

-   **__dita.xsl.xslfo.i18n-postprocess__**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    PDF I18N postprocess import

-   **__dita.xsl.xslfo__**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    Overrides the default PDF transformation. The referenced XSL file is integrated directly into the XSLT step that generates the XSL-FO.

-   **__dita.conductor.pdf2.param__**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    Pass parameters to the PDF transformation.

-   **__org.dita.pdf2.xsl.topicmerge__**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    PDF2 topic merge XSLT import

-   **__dita.catalog.plugin-info__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Plug-in XML catalog information

-   **__package.support.email__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Specifies the e-mail address of the person who provides support for the DITA-OT plug-in.

-   **__package.support.name__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Specifies the person who provides support for the DITA-OT plug-in.

-   **__package.version__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Specifies the version of the DITA-OT plug-in.

-   **__depend.preprocess.post__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target after the pre-processing stage.

-   **__depend.preprocess.pre__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the pre-processing stage.

-   **__dita.transtype.print__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Defines a transformation as a print type.

-   **__dita.resource.extensions__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Resource file extension

-   **__dita.xsl.topicpull__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Topic pull XSLT import

-   **__dita.preprocess.topicpull.param__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Topic pull XSLT parameters

-   **__depend.preprocess.topicpull.pre__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `topicpull` step in the pre-processing stage.

-   **__dita.conductor.transtype.check__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Adds a new value to the list of valid transformation types.

    **Tip:** This extension point is still supported for backwards compatibility, but since DITA-OT 2.1, any new customizations should instead use the `<transtype>` element in the [Plug-in descriptor file](../topics/plugin-configfile.md) to define a new transformation.

-   **__dita.conductor.xhtml.param__**

    Defined in plug-in [`org.dita.xhtml`](extension-points-in-org.dita.xhtml.md).

    Pass parameters to the XHTML and Eclipse Help transformations.

-   **__dita.specialization.catalog__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Adds the content of a catalog file to the main DITA-OT catalog file.

    **Attention:** This extension point is deprecated; use `dita.specialization.catalog.relative` instead.

-   **__dita.specialization.catalog.relative__**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Adds the content of a catalog file to the main DITA-OT catalog file.


