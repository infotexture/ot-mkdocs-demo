# Pre-processing extension points

You can use these extension points to run an Ant target before or after the pre-processing stage. If necessary, you can also run an Ant target before a specific pre-processing step — but this approach is not recommended.

**Tip:** For maximum compatibility with future versions of DITA-OT, most plug-ins should use the extension points that run **before** or **after** pre-processing.

-   **__depend.preprocess.pre__**

    Runs an Ant target before the pre-processing stage.

-   **__depend.preprocess.post__**

    Runs an Ant target after the pre-processing stage.


## Legacy pre-processing extensions

The following extension points are available in the original `preprocess` pipeline that was used by default for all transformations prior to DITA-OT 3.0. These extensions are not available in the newer [map-first preprocessing](../reference/map-first-preprocessing.md) pipeline \(`preprocess2`\), which is used in the PDF and HTML Help transformations as of DITA-OT 3.0.

CAUTION:

The internal order of preprocessing steps is subject to change between versions of DITA-OT. New versions may remove, reorder, combine, or add steps to the process, so the extension points **within** the preprocessing stage should only be used if absolutely necessary.

-   **__depend.preprocess.chunk.pre__**

    Runs an Ant target before the `chunk` step in the pre-processing stage.

-   **__depend.preprocess.coderef.pre__**

    Runs an Ant target before the `coderef` step in the pre-processing stage.

-   **__depend.preprocess.conref.pre__**

    Runs an Ant target before the `conref` step in the pre-processing stage.

-   **__depend.preprocess.conrefpush.pre__**

    Runs an Ant target before the `conrefpush` step in the pre-processing stage.

-   **__depend.preprocess.clean-temp.pre__**

    Runs an Ant target before the `clean-temp` step in the pre-processing stage.

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

-   **__depend.preprocess.topicpull.pre__**

    Runs an Ant target before the `topicpull` step in the pre-processing stage.


**Related information**  


[Extension points in org.dita.base](../extension-points/extension-points-in-org.dita.base.md)

