# Setting parameters with plug-ins

To ensure that output is always generated with the same settings, you can create a plug-in to define a new output format that automatically sets certain DITA-OT parameters.

You might want to build a transformation type that ensures that certain DITA-OT parameters are used. For example, consider the following scenario.

## Draft PDFs

You want to ensure that PDFs generated for internal review have the following characteristics:

-   Use company style sheets

-   Make draft comments visible to the reviewers, as they contain queries from the information developers

-   Print the file names of the graphics underneath figures, so that graphic artists can more quickly respond to requested changes


To accomplish this, you can create a new plug-in. In the Ant script that defines the transformation type, specify the DITA-OT parameters. For example, to render draft comments and art labels, add `<property>` elements to specify the DITA-OT parameters:

```
<?xml version='1.0' encoding='UTF-8'?>
<project name="com.example.draft.pdf">
  <target name="dita2draft.pdf.init">
    <property name="customization.dir"
              location="${dita.plugin.com.example.draft.pdf.dir}/cfg"/>
    **&lt;property name="args.draft" value="yes"/&gt;**
    **&lt;property name="args.artlbl" value="yes"/&gt;**
  </target>
  <target name="dita2draft.pdf"
          depends="dita2draft.pdf.init, dita2production.pdf, dita2pdf2"/>
</project>
```

