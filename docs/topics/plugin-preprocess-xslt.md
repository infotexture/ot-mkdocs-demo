# Processing topics with XSLT in preprocess

You can add an Ant target to the end of the pre-processing pipeline that transforms all topics. This is useful if you want to modify topics before transtype-specific processing, for example to modularize the code or reuse the same processing in multiple transformation types.

1.  Create a plug-in descriptor file `plugin.xml` that imports a new Ant buildfile `build.xml` and adds an Ant target after pre-processing.

    ```
    <?xml version="1.0" encoding="utf-8"?>
    <?xml-model href="https://www.dita-ot.org/rng/plugin.rnc" type="application/relax-ng-compact-syntax"?>
    <plugin id="plugin-id">
      <feature extension="ant.import" file="build.xml"/>
      <feature extension="depend.preprocess.post" value="uniform-decimals"/>
    </plugin>
    ```

2.  Create an Ant buildfile `build.xml` with a target to process all DITA topics in the temporary directory.

    ```
    <?xml version="1.0" encoding="utf-8"?>
    <project>
      <target name="uniform-decimals">
        <pipeline taskname="xslt">
          <xslt basedir="${dita.temp.dir}"
                style="${dita.plugin.plugin-id.dir}/filter.xsl">
            <ditafileset format="dita" processingRole="normal"/>
          </xslt>
        </pipeline>
      </target>
    </project>
    ```

3.  Create an XSLT stylesheet `filter.xsl` to filter topic content.

    ```
    <?xml version="1.0" encoding="utf-8"?>
    <xsl:stylesheet version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
      xmlns:xs="http://www.w3.org/2001/XMLSchema" exclude-result-prefixes="xs">
    
      <!-- Format keywords with a decimal number with at least two decimal points -->
      <xsl:template match="*[contains(@class, ' topic/keyword ')]">
        <xsl:copy>
          <xsl:apply-templates select="@*"/>
          <xsl:variable name="num" select="number(.)" as="xs:double"/>
          <xsl:choose>
            <xsl:when test="$num = $num and contains(., '.')">
              <xsl:attribute name="orig" select="."/>
              <xsl:value-of select="format-number($num, '0.00#')"/>
            </xsl:when>
            <xsl:otherwise>
              <xsl:apply-templates select="node()"/>
            </xsl:otherwise>
          </xsl:choose>
        </xsl:copy>
      </xsl:template>
    
      <!-- Identity template -->
      <xsl:template match="@* | node()">
        <xsl:copy>
          <xsl:apply-templates select="@* | node()"/>
        </xsl:copy>
      </xsl:template>
    
    </xsl:stylesheet>
    ```

4.  Use the `dita install` subcommand to install the plug-in.

    **Note:** For more information, see [Installing plug-ins](plugins-installing.md).


The `filter.xsl` stylesheet will transform every DITA topic after preprocessing.

