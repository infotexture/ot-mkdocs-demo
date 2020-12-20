# Extension points in `org.dita.base`

The `org.dita.base` plug-in provides common extension points that are available to extend processing in all transformations that DITA Open Toolkit supports. 

-   **ant.import**

    Adds an Ant import to the main Ant build file.

-   **depend.preprocess.chunk.pre**

    Runs an Ant target before the `chunk` step in the pre-processing stage.

-   **depend.preprocess.clean-temp.pre**

    Runs an Ant target before the `clean-temp` step in the pre-processing stage.

-   **depend.preprocess.coderef.pre**

    Runs an Ant target before the `coderef` step in the pre-processing stage.

-   **depend.preprocess.conref.pre**

    Runs an Ant target before the `conref` step in the pre-processing stage.

-   **depend.preprocess.conrefpush.pre**

    Runs an Ant target before the `conrefpush` step in the pre-processing stage.

-   **depend.preprocess.copy-files.pre**

    Runs an Ant target before the `copy-files` step in the pre-processing stage.

-   **depend.preprocess.copy-flag.pre**

    Runs an Ant target before the `copy-flag` step in the pre-processing stage.

-   **depend.preprocess.copy-html.pre**

    Runs an Ant target before the `copy-html` step in the pre-processing stage.

-   **depend.preprocess.copy-image.pre**

    Runs an Ant target before the `copy-image` step in the pre-processing stage.

-   **depend.preprocess.copy-subsidiary.pre**

    Runs an Ant target before the `copy-subsidiary` step in the pre-processing stage.

-   **depend.preprocess.debug-filter.pre**

    Runs an Ant target before the `debug-filter` step in the pre-processing stage.

-   **depend.preprocess.gen-list.pre**

    Runs an Ant target before the `gen-list` step in the pre-processing stage.

-   **depend.preprocess.keyref.pre**

    Runs an Ant target before the `keyref` step in the pre-processing stage.

-   **depend.preprocess.maplink.pre**

    Runs an Ant target before the `maplink` step in the pre-processing stage.

-   **depend.preprocess.mappull.pre**

    Runs an Ant target before the `mappull` step in the pre-processing stage.

-   **depend.preprocess.mapref.pre**

    Runs an Ant target before the `mapref` step in the pre-processing stage.

-   **depend.preprocess.move-meta-entries.pre**

    Runs an Ant target before the `move-meta-entries` step in the pre-processing stage.

-   **depend.preprocess.post**

    Runs an Ant target after the pre-processing stage.

-   **depend.preprocess.pre**

    Runs an Ant target before the pre-processing stage.

-   **depend.preprocess.topicpull.pre**

    Runs an Ant target before the `topicpull` step in the pre-processing stage.

-   **dita.basedir-resource-directory**

    Flag to use basedir as resource directory

-   **dita.catalog.plugin-info**

    Plug-in XML catalog information

-   **dita.conductor.lib.import**

    Adds a Java library to the DITA-OT classpath.

-   **dita.conductor.plugin**

    Ant conductor plug-in information

-   **dita.conductor.target**

    Adds an Ant import to the main Ant build file.

    **Attention:** This extension point is deprecated; use `ant.import` instead.

-   **dita.conductor.target.relative**

    Adds an Ant import to the main Ant build file.

    **Tip:** As of DITA-OT 3.0, the `ant.import` extension point can be used instead.

-   **dita.conductor.transtype.check**

    Adds a new value to the list of valid transformation types.

    **Tip:** This extension point is still supported for backwards compatibility, but since DITA-OT 2.1, any new customizations should instead use the `transtype` element in the [Plug-in descriptor file](../topics/plugin-configfile.md) to define a new transformation.

-   **dita.html.extensions**

    HTML file extension

-   **dita.image.extensions**

    Image file extension

-   **dita.parser**

    Custom DITA parser

-   **dita.preprocess.conref.param**

    Content reference XSLT parameters

-   **dita.preprocess.debug-filter.param**

    Debug filter module parameters

-   **dita.preprocess.map-reader.param**

    Debug filter module parameters

-   **dita.preprocess.mappull.param**

    Map pull XSLT parameters

-   **dita.preprocess.mapref.param**

    Map reference XSLT parameters

-   **dita.preprocess.topic-reader.param**

    Debug filter module parameters

-   **dita.preprocess.topicpull.param**

    Topic pull XSLT parameters

-   **dita.resource.extensions**

    Resource file extension

-   **dita.specialization.catalog**

    Adds the content of a catalog file to the main DITA-OT catalog file.

    **Attention:** This extension point is deprecated; use `dita.specialization.catalog.relative` instead.

-   **dita.specialization.catalog.relative**

    Adds the content of a catalog file to the main DITA-OT catalog file.

-   **dita.transtype.print**

    Defines a transformation as a print type.

-   **dita.xsl.conref**

    Content reference XSLT import

-   **dita.xsl.maplink**

    Map link XSLT import

-   **dita.xsl.mappull**

    Map pull XSLT import

-   **dita.xsl.mapref**

    Map reference XSLT import

-   **dita.xsl.messages**

    Adds new diagnostic messages to DITA-OT.

-   **dita.xsl.strings**

    Generated text

-   **dita.xsl.topicpull**

    Topic pull XSLT import

-   **package.support.email**

    Specifies the e-mail address of the person who provides support for the DITA-OT plug-in.

-   **package.support.name**

    Specifies the person who provides support for the DITA-OT plug-in.

-   **package.version**

    Specifies the version of the DITA-OT plug-in.


**Related information**  


[Pre-processing extension points](../extension-points/plugin-extension-points-pre-processing.md)

[Version and support information](../extension-points/plugin-extension-points-support.md)

[General extension points](../extension-points/plugin-extension-points-general.md)

