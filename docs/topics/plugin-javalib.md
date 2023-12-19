# Adding a Java library to the **classpath**

You can use the `dita.conductor.lib.import` extension point to add an additional Java library to the DITA-OT **classpath** parameter.

As of DITA-OT 3.1, the Java class path is managed automatically, meaning you do not \(and should not\) use explicit references to Java class paths in your build scripts. In particular, the old `dost.class.path` property has been deprecated and should not be used. If you are migrating older plug-ins that manage their class path directly, you should remove any explicit class path configuration. If your plug-in was not already using the `dita.conductor.lib.import` extension point to integrate its JAR dependencies you must add it.

The effective DITA-OT class path is the combination of the JAR files in the main `lib/` directory and the plug-in-contributed JARs, which are listed in `config/env.sh`. The `env.sh` file is updated automatically when plug-ins are installed or removed.

1.  If necessary, compile the Java code into a JAR file.

2.  Create a `plugin.xml` file that contains the following code:

    ```
    <plugin id="*plugin-id*">
      <feature extension="dita.conductor.lib.import" file="*file*"/>
    </plugin>
    ```

    where:

    -   *plugin-id* is the plug-in identifier, for example, `com.example.addjar`.
    -   *file* is the name of the JAR file, for example, `myJavaLibrary.jar`.
3.  Use the `dita install` subcommand to install the plug-in.

    **Note:** For more information, see [Installing plug-ins](plugins-installing.md).


The Ant or XSLT code now can make use of the Java code.

In the following extended example, the `myJavaLibrary.jar` file performs a validation step during processing, and you want it to run immediately before the `conref`step.

To accomplish this, you will need to use several features:

-   The JAR file must be added to the classpath.
-   The Ant target must be added to the dependency chain for conref.
-   An Ant target must be created that uses this class, and integrated into the code.

The files might look like the following:

```
<?xml version="1.0" encoding="UTF-8"?>
<plugin id="com.example.samplejava">
  *&lt;!-- Add the JAR file to the DITA-OT CLASSPATH --&gt;*
  **&lt;feature extension="dita.conductor.lib.import" 
           file="com.example.sampleValidation.jar"/&gt;**
  *&lt;!-- Integrate the Ant code --&gt;*
  <feature extension="ant.import" file="calljava-antcode.xml"/>
  *&lt;!-- Define the Ant target to call, and when \(before conref\) --&gt;*
  <feature extension="depend.preprocess.conref.pre" 
           value="validateWithJava"/>
</plugin>
```

```
<?xml version="1.0" encoding="UTF-8"?>
<project default="validateWithJava">
  <target name="validateWithJava">
    <java classname="com.example.sampleValidation">
      <!-- The class was added to the DITA-OT classpath -->
    </java>
  </target>
</project>
```

**Related information**  


[General extension points](../extension-points/plugin-extension-points-general.md)

[Installing plug-ins](../topics/plugins-installing.md)

