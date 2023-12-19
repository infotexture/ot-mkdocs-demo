# Adding an Ant target to the pre-processing pipeline

You can add an Ant target to the pre-processing pipeline. This enables you to insert additional processing before or after the pre-processing chain or a specific step in the pre-processing operation.

You can use the `depend.preprocess.pre` and `depend.preprocess.post` extension points to run a target before or after the entire pre-processing operation. In addition, there are extension points that enable you to run an Ant target before specific pre-processing steps.

**Tip:** For maximum compatibility with future versions of DITA-OT, most plug-ins should use the extension points that run **before** or **after** pre-processing.

1.  Define and integrate the new Ant target.

2.  Create the following `plugin.xml` file:

    ```
    <plugin id="*plugin-id*">
      <feature extension="*extension-point*" value="*Ant-target*"/>
    </plugin>
    ```

    where

    -   *plugin-id* is the plug-in identifier.
    -   *extension-point* is a pre-processing extension point.
    -   *Ant-target* is the name of the Ant target.
3.  Use the `dita install` subcommand to install the plug-in.

    **Note:** For more information, see [Installing plug-ins](plugins-installing.md).


The new target is added to the Ant dependency list. The new target is now always run in conjunction with the specified step in the pre-processing pipeline.

## Example

The following `plugin.xml` file specifies that the **myAntTargetBeforeChunk** target is always run before the `chunk` step in the pre-processing stage.

```
<plugin id="com.example.extendchunk">
  <feature extension="depend.preprocess.chunk.pre" 
           value="myAntTargetBeforeChunk"/>
</plugin>
```

It assumes that the **myAntTargetBeforeChunk** target has already been defined and integrated.

CAUTION:

The internal order of preprocessing steps is subject to change between versions of DITA-OT. New versions may remove, reorder, combine, or add steps to the process, so the extension points **within** the preprocessing stage should only be used if absolutely necessary.

**Related information**  


[Pre-processing extension points](../extension-points/plugin-extension-points-pre-processing.md)

[Installing plug-ins](../topics/plugins-installing.md)

