# Adding parameters to existing XSLT steps

You can pass parameters from the Ant build to existing XSLT steps in both the pre-processing pipeline and certain DITA-OT transformations. This can be useful if you want to make the parameters available as global `xsl:param` values within XSLT overrides.

1.  Create an XML file that contains one or more Ant `param` elements nested within a `dummy` wrapper element.

    ```
    <dummy>
      *<!-- Any Ant code allowed in xslt task is possible. Example: --\>*
      <param name="paramNameinXSLT" expression="${antProperty}" 
             if="antProperty"/>
    </dummy>
    ```

2.  Construct a plugin.xml file that contains the following content:

    ```
    <plugin id="plugin-id">
      <feature extension="extension-point" file="file"/>
    </plugin>
    ```

    where:

    -   plugin-id is the plug-in identifier, for example, `com.example.newparam`.
    -   extension-point is the DITA-OT extension point, for example,`dita.conductor.xhtml.param`. This indicates the DITA-OT processing step where the parameters will be available.
    -   file is the name of the XML file that you created in step [1](plugin-xsltparams.md#create-xml-file), for example, insertParameters.xml.
3.  Install the plug-in.


The plugin.xml file passes the parameters to the specified transformation or pre-processing module.

## Example

The following plug-in passes the parameters defined in the insertParameters.xml file as input to the XHTML process. Generally, an additional XSLT override will make use of the parameters to do something new with the generated content.

```
<plugin id="com.example.newparam">
  <feature extension="dita.conductor.xhtml.param" 
           file="insertParameters.xml"/>
</plugin>
```

**Related information**  


[XSLT-parameter extension points](../extension-points/plugin-extension-points-xslt-parameters.md)

[Installing plug-ins](../topics/plugins-installing.md)

