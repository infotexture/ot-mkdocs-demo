# All DITA-OT extension points

The pre-defined extension points can be used to add new functionality to DITA-OT. If your toolkit installation includes custom plug-ins that define additional extension points, you can add to this list by rebuilding the DITA-OT documentation.

-   **dita.conductor.target**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Adds an Ant import to the main Ant build file.

    **Attention:** This extension point is deprecated; use `ant.import` instead.

-   **dita.conductor.target.relative**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Adds an Ant import to the main Ant build file.

    **Tip:** As of DITA-OT 3.0, the `ant.import` extension point can be used instead.

-   **dita.conductor.plugin**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Ant conductor plug-in information

-   **ant.import**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Adds an Ant import to the main Ant build file.

-   **depend.preprocess.chunk.pre**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `chunk` step in the pre-processing stage.

-   **depend.preprocess.clean-temp.pre**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `clean-temp` step in the pre-processing stage.

-   **depend.preprocess.coderef.pre**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `coderef` step in the pre-processing stage.

-   **org.dita.pdf2.catalog.relative**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    Adds the content of a catalog file to the main catalog file for the PDF plug-in.

-   **dita.xsl.conref**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Content reference XSLT import

-   **dita.preprocess.conref.param**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Content reference XSLT parameters

-   **depend.preprocess.conref.pre**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `conref` step in the pre-processing stage.

-   **depend.preprocess.conrefpush.pre**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `conrefpush` step in the pre-processing stage.

-   **depend.preprocess.copy-html.pre**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `copy-html` step in the pre-processing stage.

-   **depend.preprocess.copy-files.pre**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `copy-files` step in the pre-processing stage.

-   **depend.preprocess.copy-flag.pre**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `copy-flag` step in the pre-processing stage.

-   **depend.preprocess.copy-image.pre**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `copy-image` step in the pre-processing stage.

-   **depend.preprocess.copy-subsidiary.pre**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `copy-subsidiary` step in the pre-processing stage.

-   **dita.parser**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Custom DITA parser

-   **depend.preprocess.debug-filter.pre**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `debug-filter` step in the pre-processing stage.

-   **dita.preprocess.debug-filter.param**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Debug filter module parameters

-   **dita.preprocess.map-reader.param**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Debug filter module parameters

-   **dita.preprocess.topic-reader.param**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Debug filter module parameters

-   **dita.xsl.messages**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Adds new diagnostic messages to DITA-OT.

-   **dita.conductor.eclipse.toc.param**

    Defined in plug-in [`org.dita.eclipsehelp`](extension-points-in-org.dita.eclipsehelp.md).

    Pass parameters to the XSLT step that generates the Eclipse Help table of contents \(TOC\).

-   **dita.xsl.eclipse.toc**

    Defined in plug-in [`org.dita.eclipsehelp`](extension-points-in-org.dita.eclipsehelp.md).

    Overrides the default XSLT step that generates the Eclipse Help table of contents \(TOC\).

-   **dita.map.eclipse.index.pre**

    Defined in plug-in [`org.dita.eclipsehelp`](extension-points-in-org.dita.eclipsehelp.md).

    Runs an Ant target before the Eclipse index extraction process.

-   **dita.xsl.eclipse.plugin**

    Defined in plug-in [`org.dita.eclipsehelp`](extension-points-in-org.dita.eclipsehelp.md).

    Overrides the default XSLT step that generates the plugin.xml file for Eclipse Help.

-   **dita.basedir-resource-directory**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Flag to use basedir as resource directory

-   **dita.conductor.pdf2.formatter.check**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    Formatter check

-   **depend.org.dita.pdf2.format.post**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    Formatting post-target

-   **depend.org.dita.pdf2.format.pre**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    Formatting pre-target

-   **depend.org.dita.pdf2.format**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    Formatting target

-   **depend.preprocess.gen-list.pre**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `gen-list` step in the pre-processing stage.

-   **dita.xsl.strings**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Generated text

-   **dita.xsl.htmlhelp.map2hhc**

    Defined in plug-in [`org.dita.htmlhelp`](extension-points-in-org.dita.htmlhelp.md).

    Overrides the default XSLT step that generates the HTML Help contents \(.hhc\) file.

-   **dita.xsl.htmlhelp.map2hhp**

    Defined in plug-in [`org.dita.htmlhelp`](extension-points-in-org.dita.htmlhelp.md).

    Overrides the default XSLT step that generates the HTML Help project \(.hhp\) file.

-   **dita.conductor.html.param**

    Defined in plug-in [`org.dita.xhtml`](extension-points-in-org.dita.xhtml.md).

    Pass parameters to the HTML and HTML Help transformations.

-   **dita.html.extensions**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    HTML file extension

-   **dita.xsl.html.cover**

    Defined in plug-in [`org.dita.xhtml`](extension-points-in-org.dita.xhtml.md).

    Overrides the default HTML cover page generation process.

-   **dita.xsl.htmltoc**

    Defined in plug-in [`org.dita.xhtml`](extension-points-in-org.dita.xhtml.md).

    Overrides the default XSLT step that generates the HTML table of contents \(TOC\).

-   **dita.xsl.xhtml**

    Defined in plug-in [`org.dita.xhtml`](extension-points-in-org.dita.xhtml.md).

    Overrides the default HTML or XHTML transformation, including HTML Help and Eclipse Help. The referenced file is integrated directly into the XSLT step that generates XHTML.

-   **dita.conductor.xhtml.toc.param**

    Defined in plug-in [`org.dita.xhtml`](extension-points-in-org.dita.xhtml.md).

    Pass parameters to the XSLT step that generates the XHTML table of contents \(TOC\).

-   **dita.conductor.html5.toc.param**

    Defined in plug-in [`org.dita.html5`](extension-points-in-org.dita.html5.md).

    Pass parameters to the XSLT step that generates the HTML5 table of contents \(TOC\).

-   **dita.xsl.html5.cover**

    Defined in plug-in [`org.dita.html5`](extension-points-in-org.dita.html5.md).

    Overrides the default HTML5 cover page generation process.

-   **dita.xsl.html5.toc**

    Defined in plug-in [`org.dita.html5`](extension-points-in-org.dita.html5.md).

    Overrides the default XSLT step that generates the HTML5 table of contents \(TOC\).

-   **dita.xsl.html5**

    Defined in plug-in [`org.dita.html5`](extension-points-in-org.dita.html5.md).

    Overrides the default HTML5 transformation. The referenced file is integrated directly into the XSLT step that generates HTML5.

-   **dita.conductor.html5.param**

    Defined in plug-in [`org.dita.html5`](extension-points-in-org.dita.html5.md).

    Pass parameters to the HTML5 transformation.

-   **dita.image.extensions**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Image file extension

-   **depend.org.dita.pdf2.index**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    Indexing target

-   **depend.org.dita.pdf2.init.pre**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    Initialization pre-target

-   **dita.conductor.lib.import**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Adds a Java library to the DITA-OT classpath.

-   **depend.preprocess.keyref.pre**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `keyref` step in the pre-processing stage.

-   **dita.xsl.maplink**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Map link XSLT import

-   **depend.preprocess.maplink.pre**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `maplink` step in the pre-processing stage.

-   **dita.preprocess.mappull.param**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Map pull XSLT parameters

-   **dita.xsl.mappull**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Map pull XSLT import

-   **depend.preprocess.mappull.pre**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `mappull` step in the pre-processing stage.

-   **dita.xsl.mapref**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Map reference XSLT import

-   **dita.preprocess.mapref.param**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Map reference XSLT parameters

-   **depend.preprocess.mapref.pre**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `mapref` step in the pre-processing stage.

-   **depend.preprocess.move-meta-entries.pre**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `move-meta-entries` step in the pre-processing stage.

-   **dita.xsl.xslfo.i18n-postprocess**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    PDF I18N postprocess import

-   **dita.xsl.xslfo**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    Overrides the default PDF transformation. The referenced XSL file is integrated directly into the XSLT step that generates the XSL-FO.

-   **dita.conductor.pdf2.param**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    Pass parameters to the PDF transformation.

-   **org.dita.pdf2.xsl.topicmerge**

    Defined in plug-in [`org.dita.pdf2`](extension-points-in-org.dita.pdf2.md).

    PDF2 topic merge XSLT import

-   **dita.catalog.plugin-info**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Plug-in XML catalog information

-   **package.support.email**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Specifies the e-mail address of the person who provides support for the DITA-OT plug-in.

-   **package.support.name**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Specifies the person who provides support for the DITA-OT plug-in.

-   **package.version**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Specifies the version of the DITA-OT plug-in.

-   **depend.preprocess.post**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target after the pre-processing stage.

-   **depend.preprocess.pre**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the pre-processing stage.

-   **dita.transtype.print**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Defines a transformation as a print type.

-   **dita.resource.extensions**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Resource file extension

-   **dita.xsl.topicpull**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Topic pull XSLT import

-   **dita.preprocess.topicpull.param**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Topic pull XSLT parameters

-   **depend.preprocess.topicpull.pre**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Runs an Ant target before the `topicpull` step in the pre-processing stage.

-   **dita.conductor.transtype.check**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Adds a new value to the list of valid transformation types.

    **Tip:** This extension point is still supported for backwards compatibility, but since DITA-OT 2.1, any new customizations should instead use the `transtype` element in the [Plug-in descriptor file](../topics/plugin-configfile.md) to define a new transformation.

-   **dita.conductor.xhtml.param**

    Defined in plug-in [`org.dita.xhtml`](extension-points-in-org.dita.xhtml.md).

    Pass parameters to the XHTML and Eclipse Help transformations.

-   **dita.specialization.catalog**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Adds the content of a catalog file to the main DITA-OT catalog file.

    **Attention:** This extension point is deprecated; use `dita.specialization.catalog.relative` instead.

-   **dita.specialization.catalog.relative**

    Defined in plug-in [`org.dita.base`](extension-points-in-org.dita.base.md).

    Adds the content of a catalog file to the main DITA-OT catalog file.


