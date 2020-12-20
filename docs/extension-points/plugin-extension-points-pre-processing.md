# Pre-processing extension points

You can use these extension points to run an Ant target before or after the pre-processing stage. If necessary, you can also run an Ant target before a specific pre-processing step — but this approach is not recommended.

**Tip:** For maximum compatibility with future versions of DITA-OT, most plug-ins should use the extension points that run **before** or **after** pre-processing.

-   **depend.preprocess.pre**

    Runs an Ant target before the pre-processing stage.

-   **depend.preprocess.post**

    Runs an Ant target after the pre-processing stage.


## Legacy pre-processing extensions

The following extension points are available in the original `preprocess` pipeline that was used by default for all transformations prior to DITA-OT 3.0. These extensions are not available in the newer [map-first preprocessing](../reference/map-first-preprocessing.md) pipeline \(`preprocess2`\), which is used in the PDF and HTML Help transformations as of DITA-OT 3.0.

CAUTION:

The internal order of preprocessing steps is subject to change between versions of DITA-OT. New versions may remove, reorder, combine, or add steps to the process, so the extension points **within** the preprocessing stage should only be used if absolutely necessary.

-   **depend.preprocess.chunk.pre**

    Runs an Ant target before the `chunk` step in the pre-processing stage.

-   **depend.preprocess.coderef.pre**

    Runs an Ant target before the `coderef` step in the pre-processing stage.

-   **depend.preprocess.conref.pre**

    Runs an Ant target before the `conref` step in the pre-processing stage.

-   **depend.preprocess.conrefpush.pre**

    Runs an Ant target before the `conrefpush` step in the pre-processing stage.

-   **depend.preprocess.clean-temp.pre**

    Runs an Ant target before the `clean-temp` step in the pre-processing stage.

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

-   **depend.preprocess.topicpull.pre**

    Runs an Ant target before the `topicpull` step in the pre-processing stage.


**Related information**  


[Extension points in org.dita.base](../extension-points/extension-points-in-org.dita.base.md)

