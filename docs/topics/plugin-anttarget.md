# Adding a new target to the Ant build process

As of DITA-OT 3.0, the `ant.import` extension point can be used to make new targets available to the Ant processing pipeline. This can be done as part of creating a new transformation, extending pre-processing, or simply to make new Ant targets available to other plug-ins.

1.  Create an Ant project file that contains the new target\(s\).

2.  Create the plugin.xml file:

    ```
    <plugin id="plugin-id">
      <feature extension="ant.import" file="build-file"/>
    </plugin>
    ```

    where:

    -   plugin-id is the plug-in identifier, for example, `com.example.ant`.
    -   build-file is the Ant project file that contains the new build target\(s\).
3.  Install the plug-in.


The targets from the project \(build-file\) are copied into the build.xml file, using the correct path. This makes the new Ant targets available to other processes.

**Tip:** Earlier versions of DITA-OT use the `dita.conductor.target.relative` to call a wrapper file with a dummy task that imports the Ant project file. This approach is still supported for backwards compatibility, but the simpler `ant.import` approach described above should be used for all new customizations.

**Related information**  


[General extension points](../extension-points/plugin-extension-points-general.md)

[Installing plug-ins](../topics/plugins-installing.md)

