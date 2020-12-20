# Referencing files from other plug-ins

Starting with DITA-OT 1.5.4, you can use the plugin:plugin-id URI extension and the $\{dita.plugin.plugin-id.dir\} Ant variable to reference the base path of another installed DITA-OT plug-in.

Sometimes you need to reference content in another DITA-OT plug-in. However, the path to an installed plug-in is not guaranteed to be the same between different installed instances of DITA-OT. The plugin:plugin-id URI extension and $\{dita.plugin.plugin-id.dir\} Ant variable are provided so your build and XSLT files always use the correct path to the plug-in.

Within a single plug-in, you can safely use relative path references, for example, xsl/my.xsl without specifying the path to the plug-in itself.

-   Use $\{dita.plugin.plugin-id.dir\} in Ant build files.

    Use the Ant variable $\{dita.plugin.plugin-id.dir\} anywhere in your build file or template to point to the base path of an installed DITA-OT plug-in.

    The following example copies CSS files from the HTML5 plug-in:

    ```
    <copy todir="${dita.temp.dir}/css">
      <fileset dir="${dita.plugin.org.dita.html5.dir}/css" 
               includes="*.css"/>
    </copy>
    ```

-   Use plugin:plugin-id in XSLT files.

    Use the URI extension plugin:plugin-id at the beginning of a file reference—usually in `xsl:import`—to point to the base path of an installed DITA-OT plug-in.

    The following example imports the base output-message.xsl processing:

    ```language-xml
    <xsl:import href="plugin:org.dita.base:xsl/common/output-message.xsl"/>
    ```

    To use the URI extension, your plug-in must reference the DITA-OT catalog file. In your Ant build file, add an `xmlcatalog` element referencing the DITA-OT catalog file as a child of the `xslt` element.

    ```
    <xslt style="xsl/my.xsl"
          in="${dita.temp.dir}/input.file" 
          out="${dita.temp.dir}/output.file">
      <xmlcatalog refid="dita.catalog"/>
    </xslt>
    ```


For both of these methods, make sure you use the plug-in ID \(defined in the plugin.xml file\) rather than the folder name of the plug-in. In many cases, the folder name is not the same as the plug-in ID.

**Related information**  


[Plug-in coding conventions](../topics/plugin-coding-conventions.md)

