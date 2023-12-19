# Overriding an XSLT-processing step

You can override specific XSLT-processing steps in both the pre-processing pipeline and certain DITA-OT transformations.

1.  Develop an XSL file that contains the XSL override.

2.  Construct a `plugin.xml` file that contains the following content:

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <plugin id="*plugin-id*">
      <feature extension="*extension-point*" file="*relative-path*"/>
    </plugin>
    ```

    where:

    -   *plugin-id* is the plug-in identifier, for example, com.example.brandheader.
    -   *extension-point* is the DITA-OT extension point, for example,`dita.xsl.xhtml`. This indicates the DITA-OT processing step that the XSL override applies to.
    -   *relative-path* is the relative path and name of the XSLT file, for example, `xsl/header.xsl`.
3.  Use the `dita install` subcommand to install the plug-in.

    **Note:** For more information, see [Installing plug-ins](plugins-installing.md).


The plug-in installer adds an XSL import statement to the default DITA-OT code, so that the XSL override becomes part of the normal build.

## Example: Overriding XHTML header processing

The following two files represent a complete, simple style plug-in.

The `plugin.xml` file declares an XSLT file that extends XHTML processing:

```
<?xml version="1.0" encoding="UTF-8"?>
<plugin id="com.example.brandheader">
  <feature extension="dita.xsl.xhtml" file="xsl/header.xsl"/>
</plugin>
```

The `xsl/header.xsl` XSLT file referenced in `plugin.xml` overrides the default header processing to add a banner:

```
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="1.0" 
                xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:template name="gen-user-header">
    <div><img src="http://www.example.com/company_banner.jpg" 
              alt="Example Company Banner"/></div>
  </xsl:template>
</xsl:stylesheet>
```

**Related information**  


[XSLT-import extension points](../extension-points/plugin-extension-points-xslt-import.md)

[Installing plug-ins](../topics/plugins-installing.md)

