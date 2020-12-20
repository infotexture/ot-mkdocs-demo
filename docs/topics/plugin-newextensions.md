# Creating a new plug-in extension point

If your plug-in needs to define its own extension points in an XML file, add the string "`_template`" to the filename before the file suffix. When the plug-in is installed, this file will be processed like the built-in DITA-OT templates.

Template files are used to integrate most DITA-OT extensions. For example, the dita2xhtml\_template.xsl file contains all of the default rules for converting DITA topics to XHTML, along with an extension point for plug-in extensions. When the plug-in is installed, the dita2xhtml.xsl is recreated, and the extension point is replaced with references to all appropriate plug-ins.

To mark a new file as a template file, use the `template` element.

The template extension namespace has the URI `http://dita-ot.sourceforge.net`. It is used to identify elements and attributes that have a special meaning in template processing. This documentation uses the `dita:` prefix to refer to elements in the template extension namespace. However, template files are free to use any prefix, provided that there is a namespace declaration that binds the prefix to the URI of the template extension namespace.

## `dita:extension` element

The `dita:extension` elements are used to insert generated content during the plug-in installation process. There are two required attributes:

-   The `@id` attribute defines the extension point ID that provides the argument data.
-   The `@behavior` attribute defines which processing action is used.

Supported values for the `@behavior` attribute:

-   **`org.dita.dost.platform.CheckTranstypeAction`**

    Create Ant condition elements to check if the `${transtype}` property value equals a supported transformation type value.

-   **`org.dita.dost.platform.ImportAntLibAction`**

    Create Ant `pathelement` elements for the [library import extension point](plugin-javalib.md). The `@id` attribute is used to define the extension point ID.

-   **`org.dita.dost.platform.ImportPluginCatalogAction`**

    Include plug-in metadata catalog content.

-   **`org.dita.dost.platform.ImportPluginInfoAction`**

    Create plug-in metadata Ant properties.

-   **`org.dita.dost.platform.ImportStringsAction`**

    Include plug-in string file content based on the [generated text extension point](plugin-addgeneratedtext.md). The `@id` attribute is used to define the extension point ID.

-   **`org.dita.dost.platform.ImportXSLAction`**

    Create `xsl:import` elements based on the [XSLT import extension point](plugin-overridestyle.md). The `@id` attribute is used to define the extension point ID.

-   **`org.dita.dost.platform.InsertAction`**

    Include plug-in conductor content based on the [Ant import extension point](plugin-anttarget.md). The `@id` attribute is used to define the extension point ID.

-   **`org.dita.dost.platform.InsertAntActionRelative`**

    Include plug-in conductor content based on the [relative Ant import extension point](plugin-anttarget.md). The `@id` attribute is used to define the extension point ID.

-   **`org.dita.dost.platform.InsertCatalogActionRelative`**

    Include plug-in catalog content based on the [catalog import extension point](plugin-xmlcatalog.md). The `@id` attribute is used to define the extension point ID.

-   **`org.dita.dost.platform.ListTranstypeAction`**

    Create a pipe-delimited list of supported transformation types.


## `@dita:extension` attribute

The `@dita:extension` attribute is used to process attributes in elements which are not in the template extension namespace. The value of the attribute is a space-delimited tuple, where the first item is the name of the attribute to process and the second item is the action ID.

Supported values:

-   **`depends org.dita.dost.platform.InsertDependsAction`**

    The Ant target dependency list is processed to replace all target names that start with an opening brace `{` character and end with a closing brace `}`. The value of the extension point is the ID between the braces.


## Example

The following plug-in defines myBuildFile\_template.xml as a new template for extensions, and two new extension points.

```
<plugin id="com.example.new-extensions">
  <extension-point id="com.example.new-extensions.pre"
                   name="Custom target preprocess"/>
  <extension-point id="com.example.new-extensions.content"
                   name="Custom target content"/>
  <template file="myBuildFile_template.xml"/>
</plugin>
```

When the plug-in is installed, this will be used to recreate myBuildFile.xml, replacing Ant file content based on extension point use.

```
<project xmlns:dita="http://dita-ot.sourceforge.net">
  <target name="dita2custom"
     dita:depends="dita2custom.init,
                  {com.example.new-extensions.pre},
                   dita2xhtml"
     dita:extension="depends org.dita.dost.platform.InsertDependsAction">
    <dita:extension id="com.example.new-extensions.content"
                    behavior="org.dita.dost.platform.InsertAction"/>
  </target>
</project>
```

