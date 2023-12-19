# Example: Creating a simple PDF plug-in

This scenario walks through the process of creating a very simple plug-in \(`com.example.print-pdf`\) that creates a new transformation type: print-pdf.

The print-pdf transformation has the following characteristics:

-   Uses A4 paper
-   Renders figures with a title at the top and a description at the bottom
-   Removes the period after the number for an ordered-list item
-   Use em dashes as the symbols for unordered lists

1.  In the `plugins` directory, create a directory named `com.example.print-pdf`.

2.  In the new `com.example.print-pdf` directory, create a plug-in configuration file \(`plugin.xml`\) that declares the new print-pdf transformation and its dependencies.

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

3.  Add an Ant script \(`integrator.xml`\) to define the transformation type.

    ```
    <?xml version='1.0' encoding='UTF-8'?>
    <project>
      <target name="dita2print-pdf"
           depends="dita2print-pdf.init,
                    dita2pdf2"/>
      <target name="dita2print-pdf.init">
        <property name="customization.dir"
              location="${dita.plugin.com.example.print-pdf.dir}/cfg"/>
       </target>
    </project>
    ```

4.  In the new plug-in directory, add a `cfg/catalog.xml` file that specifies the custom XSLT style sheets.

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <catalog prefer="system"
             xmlns="urn:oasis:names:tc:entity:xmlns:xml:catalog">
      <uri name="cfg:fo/attrs/custom.xsl" uri="fo/attrs/custom.xsl"/>
      <uri name="cfg:fo/xsl/custom.xsl" uri="fo/xsl/custom.xsl"/>
    </catalog>
    ```

5.  Create the `cfg/fo/attrs/custom.xsl` file, and add attribute and variable overrides to it.

    For example, add the following variables to change the page size to A4.

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
                    version="2.0">
      <!-- Change page size to A4 -->
      <xsl:variable name="page-width">210mm</xsl:variable>
      <xsl:variable name="page-height">297mm</xsl:variable>
    </xsl:stylesheet>
    ```

6.  Create the `cfg/fo/xsl/custom.xsl` file, and add XSLT overrides to it.

    For example, the following code changes the rendering of `<figure>` elements.

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
                    xmlns:xs="http://www.w3.org/2001/XMLSchema"
                    xmlns:fo="http://www.w3.org/1999/XSL/Format"
                    version="2.0">
      <!-- Move figure title to top and description to bottom -->
      <xsl:template match="*[contains(@class,' topic/fig ')]">
        <fo:block xsl:use-attribute-sets="fig">
          <xsl:call-template name="commonattributes"/>
          <xsl:if test="not(@id)">
            <xsl:attribute name="id">
              <xsl:call-template name="get-id"/>
            </xsl:attribute>
          </xsl:if>
          <xsl:apply-templates select="*[contains(@class,' topic/title ')]"/>
          <xsl:apply-templates select="*[not(contains(@class,' topic/title ') or contains(@class,' topic/desc '))]"/>
          <xsl:apply-templates select="*[contains(@class,' topic/desc ')]"/>
        </fo:block>
      </xsl:template>
    </xsl:stylesheet>
    ```

7.  Create an English-language variable-definition file \(`cfg/common/vars/en.xml`\) and make any necessary modifications to it.

    For example, the following code removes the period after the number for an ordered-list item; it also specifies that the bullet for an unordered list item should be an em dash.

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <variables>
      <!-- Remove dot from list number -->
      <variable id="Ordered List Number 1">
        <param ref-name="number"/>
      </variable>
      <!-- Change unordered list bullet to an em dash -->
      <variable id="Unordered List bullet 1">&#x2014;</variable>
    </variables>
    ```


**Tip:** The files for this sample plug-in are included in the DITA-OT installation directory under `docsrc/samples/plugins/com.example.print-pdf/` and on [GitHub](https://github.com/dita-ot/docs/tree/develop/samples/plugins/com.example.print-pdf).

The plug-in directory has the following layout and files:

```
com.example.print-pdf
├── cfg
│   ├── catalog.xml
│   ├── common
│   │   └── vars
│   │       └── en.xml
│   └── fo
│       ├── attrs
│       │   └── custom.xsl
│       └── xsl
│           └── custom.xsl
├── integrator.xml
└── plugin.xml
```

1.  Use the `dita install` subcommand to install the plug-in.

    **Note:** For more information, see [Installing plug-ins](plugins-installing.md).

2.  Build output with the new transformation type to verify that the plug-in works as intended.

    ```
    ``dita`` **--input**=*my.ditamap* **--format**=print-pdf
    ```


**Related information**  


[Installing plug-ins](../topics/plugins-installing.md)

