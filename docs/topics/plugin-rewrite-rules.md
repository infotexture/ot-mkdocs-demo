# Adjusting file names in map-first pre-processing

To dynamically adjust the names and locations of output files in the map-first pre-processing routine \(`preprocess2`\), you can create a custom plug-in and specify the code that contains your custom rewrite rules.

For example, set the **result.rewrite-rule.xsl** parameter to specify a bundled XSLT stylesheet that contains your custom rewrite rules.

```
<?xml version='1.0' encoding='UTF-8'?>
<project name="com.example.rewrite.pdf">
  <target name="dita2rewrite.pdf.init">
    <property name="customization.dir"
              location="${dita.plugin.com.example.rewrite.pdf.dir}/cfg"/>
    **&lt;property name="result.rewrite-rule.xsl" 
              value="$\{dita.plugin.com.example.rewrite.pdf.dir\}/custom-rules.xsl"/&gt;**
  </target>
  <target name="dita2rewrite.pdf"
          depends="dita2rewrite.pdf.init, dita2production.pdf, dita2pdf2"/>
</project>
```

Your plug-in would also include a `custom-rules.xsl` file, which might contain templates like this to move all image files to an `images` subdirectory:

```
<xsl:template match="node() | @*">
  <xsl:copy>
    <xsl:apply-template select="node() | @*"/>
  </xsl:copy>
</xsl:template>

<xsl:template match="file[@format = 'image']/@result">
  <xsl:attribute name="{local-name()}" select="concat('images/', .)"/>
</xsl:template>
```

**Note:** If your rewrite rules are contained in a Java class, you can set the **result.rewrite-rule.class** parameter instead, and pass the name of your Java class in the `@value attribute.` The custom class should implement the `org.dita.dost.module.RewriteRule` interface.

