# Embedding web fonts in HTML output

A custom plug-in can be created to generate HTML output that uses custom fonts for enhanced typographic features, extended character sets or a unique corporate identity.

This scenario walks through the process of creating a very simple plug-in \(`com.example.html5-webfont`\) that creates a new transformation type: html5-webfont.

The html5-webfont transformation includes a custom CSS file and sets five parameters to integrate font links and a custom stylesheet in the generated HTML5 output. These parameter settings make the following changes:

-   Specify a file that links to the font from the document head with args.hdf.

-   Specify the css subfolder of the plug-in as the source directory for custom CSS with args.cssroot.

-   Specify the name of the custom CSS file with args.css.

    The value of this parameter tells DITA-OT to use the custom.css file provided by the plug-in.

-   Ensure that the CSS file is copied to the output directory by setting args.copycss to yes.

-   Set the destination path for CSS files in the output folder with args.csspath.

    CSS files are copied to the root level of the output folder by default. Setting this parameter places CSS files in a dedicated css subfolder.


All five parameters are set in the Ant script \(build\_html5-webfont.xml\).

1.  In the plugins directory, create a directory named com.example.html5-webfont.

2.  In the new com.example.html5-webfont directory, create a plug-in configuration file \(plugin.xml\) that declares the new html5-webfont transformation and its dependencies.

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <?xml-model href="https://www.dita-ot.org/rng/plugin.rnc" type="application/relax-ng-compact-syntax"?>
    
    <plugin id="com.example.html5-webfont">
      <require plugin="org.dita.html5"/>
      <transtype name="html5-webfont" extends="html5" desc="HTML5 with Noto Sans webfont"/>
      <feature extension="ant.import" file="build_html5-webfont.xml"/>
    </plugin>
    ```

    **Note:** This plug-in will extend the default HTML5 transformation, so the `require` element explicitly defines org.dita.html5 as a dependency.

3.  In the com.example.html5-webfont directory, create a subdirectory named include.

4.  In the new include subdirectory, create a file named webfont.hdf.xml with your custom font links.

    ```
    <div>
      <link href="https://fonts.googleapis.com/css?family=Noto+Sans" rel="stylesheet"/>
    </div>
    ```

    This example uses the [Noto Sans](https://fonts.google.com/specimen/Noto+Sans) font. You can use multiple fonts by creating additional `link` references in this file. The division wrapper will be discarded when generating HTML files, and the contents will be inserted into the `head` element of each page.

5.  In the com.example.html5-webfont directory, create a subdirectory named css.

6.  In the new css subdirectory, create a file named custom.css with the stylesheet rules that apply the custom `font-family` to the desired elements.

    ```
    body {
      font-family: 'Noto Sans', sans-serif;
    }
    ```

    This example uses [Noto Sans](https://fonts.google.com/specimen/Noto+Sans) for all body content. In practice, you would normally use different fonts for headings, body content, tables, etc. by creating additional rules in your CSS file.

7.  In the com.example.html5-webfont root directory, add an Ant script \(build\_html5-webfont.xml\) to define the transformation type.

    ```
    <?xml version='1.0' encoding='UTF-8'?>
    
    <project>
      <target name="dita2html5-webfont"
           depends="dita2html5-webfont.init,
                    dita2html5"/>
      <target name="dita2html5-webfont.init">
        <property name="args.hdf"
              location="${dita.plugin.com.example.html5-webfont.dir}/include/webfont.hdf.xml"/>
        <property name="args.cssroot"
              location="${dita.plugin.com.example.html5-webfont.dir}/css"/>
        <property name="args.css" value="custom.css"/>
        <property name="args.copycss" value="yes"/>
        <property name="args.csspath" value="css"/>
      </target>
    </project>
    ```


**Tip:** The files for this sample plug-in are included in the DITA-OT installation directory under docsrc/samples/plugins/com.example.html5-webfont/ and on [GitHub](https://github.com/dita-ot/docs/tree/develop/samples/plugins/com.example.html5-webfont).

The plug-in directory has the following layout and files:

```
com.example.html5-webfont
├── build_html5-webfont.xml
├── css
│   └── custom.css
├── include
│   └── webfont.hdf.xml
└── plugin.xml
```

1.  Run dita --install to install the plug-in and make the html5-webfont transformation available.
2.  Build output with the new transformation type to verify that the plug-in works as intended.

    ```
    dita --input=my.ditamap --format=html5-webfont
    ```

3.  Refine the styles in your custom.css file to adjust the font usage as necessary.

**Related information**  


[HTML-based output parameters](../parameters/parameters-base-html.md)

