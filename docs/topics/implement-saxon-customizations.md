# Adding Saxon customizations

Plug-ins can contribute XSLT extension functions and collation URI resolvers. These customizations are automatically configured to work with Saxon when transformations are run using the DITA-OT `<pipeline>` task with custom XSLT.

Plug-ins can provide the following Saxon extensions:

-   Extension functions
-   Collation URI resolvers

Extensions are declared in plug-in-provided JAR files using the Java ServiceLoader feature that looks for service-declaring files in JAR files and loads classes. This requires adding one or more files in the `META-INF/services` directory in plug-in-provided JAR files.

You can create the file manually or generate it dynamically using `<service>` elements in Ant `<jar>` tasks. See the topics for the different extension types for details.

These extensions use the DITA Open Toolkit Ant `<pipeline>` element to wrap `<xslt>` elements. You can do this in plug-ins as shown in this excerpt from the DITA Community I18N plugin’s `build.xml` file:

```language-xml
<target name="org.dita-community.i18n-saxon-extension-test">
  <pipeline message="Test the DITA Community i18n Saxon extension functions"
            taskname="i18n-extension-function-test">
    <xslt
      in="${dita.plugin.org.dita-community.i18n.dir}/test/xsl/data/test-data.xml"
      style="${dita.plugin.org.dita-community.i18n.dir}/test/xsl/test-extension-functions.xsl"
      out="${basedir}/out/extension-function-test-results.xml"
      >
    </xslt>
  </pipeline>
</target>
```

Normal XSLT extensions to built-in transformation types will automatically have the extensions available to them.

The dynamic Saxon configuration is implemented in the class `org.dita.dost.module.XsltModule`, which backs the `<pipeline>`/`<xslt>` element.



