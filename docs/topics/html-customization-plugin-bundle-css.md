# Bundling CSS in a custom HTML plug-in

You can create a DITA-OT plug-in that provides a custom stylesheet with the typography and colors that define your corporate identity. Coworkers can install this plug-in to ensure consistent HTML output across projects without having to copy the stylesheet to each project.

This scenario walks through the process of creating a very simple plug-in \(`com.example.html5-custom-css`\) that creates a new transformation type: html5-custom-css.

The html5-custom-css transformation includes a custom CSS file and sets four parameters to integrate the custom stylesheet in the generated HTML5 output. These parameter settings make the following changes:

-   Specify the `css` subfolder of the plug-in as the source directory for custom CSS with **args.cssroot**.

-   Specify the name of the custom CSS file with **args.css**.

    The value of this parameter tells DITA-OT to use the `custom.css` file provided by the plug-in.

-   Ensure that the CSS file is copied to the output directory by setting **args.copycss** to yes.

-   Set the destination path for CSS files in the output folder with **args.csspath**.

    CSS files are copied to the root level of the output folder by default. Setting this parameter places CSS files in a dedicated `css` subfolder.


All four parameters are set in the Ant script \(`build_html5-custom-css.xml`\).

1.  In the `plugins` directory, create a directory named `com.example.html5-custom-css`.

2.  In the new `com.example.html5-custom-css` directory, create a plug-in configuration file \(`plugin.xml`\) that declares the new html5-custom-css transformation and its dependencies.

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <?xml-model href="https://www.dita-ot.org/rng/plugin.rnc" type="application/relax-ng-compact-syntax"?>
    
    <plugin id="com.example.html5-custom-css">
      <require plugin="org.dita.html5"/>
      <transtype name="html5-custom-css" extends="html5" desc="HTML5 with custom CSS"/>
      <feature extension="ant.import" file="build_html5-custom-css.xml"/>
    </plugin>
    ```

    **Note:** This plug-in will extend the default HTML5 transformation, so the `<require>` element explicitly defines `org.dita.html5` as a dependency.

3.  In the `com.example.html5-custom-css` directory, create a subdirectory named `css`.

4.  In the new `css` subdirectory, create a file named `custom.css` with your custom CSS rules.

    ```
    /* These custom styles extend or override DITA Open Toolkit default styles. */
    
    body {
      color: #F00;
    }
    ```

    **Tip:** When you first create the plug-in, you may want to include a rule in your custom stylesheet that makes it readily apparent when the custom styles are applied \(the example above will change body text to “red”\). Once you have verified that the plug-in works as intended, replace the placeholder rule with your own custom styles.

5.  In the `com.example.html5-custom-css` root directory, add an Ant script \(`build_html5-custom-css.xml`\) to define the transformation type.

    ```
    <?xml version='1.0' encoding='UTF-8'?>
    
    <project>
      <target name="dita2html5-custom-css"
           depends="dita2html5-custom-css.init,
                    dita2html5"/>
      <target name="dita2html5-custom-css.init">
        <property name="args.cssroot"
              location="${dita.plugin.com.example.html5-custom-css.dir}/css"/>
        <property name="args.css" value="custom.css"/>
        <property name="args.copycss" value="yes"/>
        <property name="args.csspath" value="css"/>
      </target>
    </project>
    ```


**Tip:** The files for this sample plug-in are included in the DITA-OT installation directory under `docsrc/samples/plugins/com.example.html5-custom-css/` and on [GitHub](https://github.com/dita-ot/docs/tree/develop/samples/plugins/com.example.html5-custom-css).

The plug-in directory has the following layout and files:

```
com.example.html5-custom-css
├── build_html5-custom-css.xml
├── css
│   └── custom.css
└── plugin.xml
```

1.  Use the `dita install` subcommand to install the plug-in.

    **Note:** For more information, see [Installing plug-ins](plugins-installing.md).

2.  Build output with the new transformation type to verify that the plug-in works as intended.

    ```
    ``dita`` **--input**=*my.ditamap* **--format**=html5-custom-css
    ```

3.  Refine the styles in your `custom.css` file as necessary.

**Related information**  


[HTML-based output parameters](../parameters/parameters-base-html.md)

[Adding custom CSS](../topics/html-customization-css.md)

