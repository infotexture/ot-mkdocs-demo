# Adding a new transformation type

Plug-ins can add an entirely new transformation type. The new transformation type can be very simple, such as an HTML build that creates an additional control file; it also can be very complex, adding any number of new processing steps.

You can use the `transtype` element to define a new transformation type with any new custom parameters that are supported.

When a transformation type is defined, the build expects Ant code to be integrated to define the transformation process. The Ant code must define a target based on the name of the transformation type; if the transformation type is "new-transform", the Ant code must define a target named dita2new-transform.

1.  Create an Ant project file for the new transformation. This project file must define a target named "dita2new-transtype," where new-transtype is the name of the new transformation type.

2.  Create a plugin.xml with the following content:

    ```
    <plugin id="plugin-id">
      <transtype name="new-transtype"/>
      **&lt;feature extension="dita.transtype.print" value="new-transtype"/&gt;**
      <feature extension="ant.import" file="ant-file"/>
    </plugin>
    ```

    where:

    -   plugin-id is the plug-in identifier, for example, com.dita-ot.pdf.
    -   new-transtype is the name of the new transformation, for example, dita-ot-pdf.
    -   ant-file is the name of the Ant file, for example, build-dita-ot-pdf.xml.
    Exclude the content that is highlighted in bold if the transformation is not intended for print.

3.  Install the plug-in.


You now can use the new transformation.

## Examples

The following plugin.xml file defines a new transformation type named "print-pdf"; it also defines the transformation type to be a print type. The build will look for a dita2print-pdf target.

```
<?xml version="1.0" encoding="UTF-8"?>
<?xml-model href="https://www.dita-ot.org/rng/plugin.rnc" type="application/relax-ng-compact-syntax"?>

<plugin id="com.example.print-pdf">
  <require plugin="org.dita.pdf2"/>
  <transtype name="print-pdf" extends="pdf" desc="PDF on A4 paper"/>
  <feature extension="dita.transtype.print" value="print-pdf"/>
  <feature extension="ant.import" file="integrator.xml"/>
</plugin>
```

**Tip:** For a complete sample plug-in with all required code, see [Example: Creating a simple PDF plug-in](pdf-customization-example.md).

If your custom transformation type supports custom parameters, they can be defined in nested `param` elements within the `transtype` element.

While the org.dita.html5 plug-in was separated from `common-html` in version 2.4, the following example shows how earlier versions of that plug-in used the `transtype` element to extend the common HTML transformation with a new html5 transformation type and define a new nav-toc parameter with three possible values:

```
**&lt;transtype name="html5" extends="common-html" desc="HTML5"&gt;**
  <param name="nav-toc" type="enum" 
         desc="Specifies whether to generate navigation in topic pages.">
    <val default="true" desc="No TOC">none</val>
    <val desc="Partial TOC that shows the current topic">partial</val>
    <val desc="Full TOC">full</val>
  </param>
</transtype>
```

**Related information**  


[General extension points](../extension-points/plugin-extension-points-general.md)

[Plug-in descriptor file](../topics/plugin-configfile.md)

[Installing plug-ins](../topics/plugins-installing.md)

