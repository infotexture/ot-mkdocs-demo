# Extension points in `org.dita.base`

The `org.dita.base` plug-in provides common extension points that are available to extend processing in all transformations that DITA Open Toolkit supports. 

-   **__ant.import__**

    Adds an Ant import to the main Ant build file.

-   **__depend.preprocess.chunk.pre__**

    Runs an Ant target before the `chunk` step in the pre-processing stage.

-   **__depend.preprocess.clean-temp.pre__**

    Runs an Ant target before the `clean-temp` step in the pre-processing stage.

-   **__depend.preprocess.coderef.pre__**

    Runs an Ant target before the `coderef` step in the pre-processing stage.

-   **__depend.preprocess.conref.pre__**

    Runs an Ant target before the `conref` step in the pre-processing stage.

-   **__depend.preprocess.conrefpush.pre__**

    Runs an Ant target before the `conrefpush` step in the pre-processing stage.

-   **__depend.preprocess.copy-files.pre__**

    Runs an Ant target before the `copy-files` step in the pre-processing stage.

-   **__depend.preprocess.copy-flag.pre__**

    Runs an Ant target before the `copy-flag` step in the pre-processing stage.

-   **__depend.preprocess.copy-html.pre__**

    Runs an Ant target before the `copy-html` step in the pre-processing stage.

-   **__depend.preprocess.copy-image.pre__**

    Runs an Ant target before the `copy-image` step in the pre-processing stage.

-   **__depend.preprocess.copy-subsidiary.pre__**

    Runs an Ant target before the `copy-subsidiary` step in the pre-processing stage.

-   **__depend.preprocess.debug-filter.pre__**

    Runs an Ant target before the `debug-filter` step in the pre-processing stage.

-   **__depend.preprocess.gen-list.pre__**

    Runs an Ant target before the `gen-list` step in the pre-processing stage.

-   **__depend.preprocess.keyref.pre__**

    Runs an Ant target before the `keyref` step in the pre-processing stage.

-   **__depend.preprocess.maplink.pre__**

    Runs an Ant target before the `maplink` step in the pre-processing stage.

-   **__depend.preprocess.mappull.pre__**

    Runs an Ant target before the `mappull` step in the pre-processing stage.

-   **__depend.preprocess.mapref.pre__**

    Runs an Ant target before the `mapref` step in the pre-processing stage.

-   **__depend.preprocess.move-meta-entries.pre__**

    Runs an Ant target before the `move-meta-entries` step in the pre-processing stage.

-   **__depend.preprocess.post__**

    Runs an Ant target after the pre-processing stage.

-   **__depend.preprocess.pre__**

    Runs an Ant target before the pre-processing stage.

-   **__depend.preprocess.topicpull.pre__**

    Runs an Ant target before the `topicpull` step in the pre-processing stage.

-   **__dita.basedir-resource-directory__**

    Flag to use basedir as resource directory

-   **__dita.catalog.plugin-info__**

    Plug-in XML catalog information

-   **__dita.conductor.lib.import__**

    Adds a Java library to the DITA-OT classpath.

-   **__dita.conductor.plugin__**

    Ant conductor plug-in information

-   **__dita.conductor.target__**

    Adds an Ant import to the main Ant build file.

    **Attention:** This extension point is deprecated; use `ant.import` instead.

-   **__dita.conductor.target.relative__**

    Adds an Ant import to the main Ant build file.

    **Tip:** As of DITA-OT 3.0, the `ant.import` extension point can be used instead.

-   **__dita.conductor.transtype.check__**

    Adds a new value to the list of valid transformation types.

    **Tip:** This extension point is still supported for backwards compatibility, but since DITA-OT 2.1, any new customizations should instead use the `<transtype>` element in the [Plug-in descriptor file](../topics/plugin-configfile.md) to define a new transformation.

-   **__dita.html.extensions__**

    HTML file extension

-   **__dita.image.extensions__**

    Image file extension

-   **__dita.parser__**

    Custom DITA parser

-   **__dita.preprocess.conref.param__**

    Content reference XSLT parameters

-   **__dita.preprocess.debug-filter.param__**

    Debug filter module parameters

-   **__dita.preprocess.map-reader.param__**

    Debug filter module parameters

-   **__dita.preprocess.mappull.param__**

    Map pull XSLT parameters

-   **__dita.preprocess.mapref.param__**

    Map reference XSLT parameters

-   **__dita.preprocess.topic-reader.param__**

    Debug filter module parameters

-   **__dita.preprocess.topicpull.param__**

    Topic pull XSLT parameters

-   **__dita.resource.extensions__**

    Resource file extension

-   **__dita.specialization.catalog__**

    Adds the content of a catalog file to the main DITA-OT catalog file.

    **Attention:** This extension point is deprecated; use `dita.specialization.catalog.relative` instead.

-   **__dita.specialization.catalog.relative__**

    Adds the content of a catalog file to the main DITA-OT catalog file.

-   **__dita.transtype.print__**

    Defines a transformation as a print type.

-   **__dita.xsl.conref__**

    Content reference XSLT import

-   **__dita.xsl.maplink__**

    Map link XSLT import

-   **__dita.xsl.mappull__**

    Map pull XSLT import

-   **__dita.xsl.mapref__**

    Map reference XSLT import

-   **__dita.xsl.messages__**

    Adds new diagnostic messages to DITA-OT.

-   **__dita.xsl.strings__**

    Generated text

-   **__dita.xsl.topicpull__**

    Topic pull XSLT import

-   **__package.support.email__**

    Specifies the e-mail address of the person who provides support for the DITA-OT plug-in.

-   **__package.support.name__**

    Specifies the person who provides support for the DITA-OT plug-in.

-   **__package.version__**

    Specifies the version of the DITA-OT plug-in.


**Related information**  


[Pre-processing extension points](../extension-points/plugin-extension-points-pre-processing.md)

[Version and support information](../extension-points/plugin-extension-points-support.md)

[General extension points](../extension-points/plugin-extension-points-general.md)

