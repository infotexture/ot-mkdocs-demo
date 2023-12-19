# Inserting JavaScript in generated HTML

JavaScript code can be bundled in a custom plug-in and automatically inserted into the generated HTML pages to enable web analytics or dynamic content delivery.

This scenario walks through the process of creating a very simple plug-in \(`com.example.html5-javascript`\) that creates a new transformation type: html5-javascript.

The html5-javascript transformation includes a custom page footer file with a JavaScript tracking snippet and sets the **args.ftr** parameter to integrate the script content in the HTML5 `<footer>` element of the generated pages.

**Note:** This example inserts a tracking snippet for Google Analytics, but the basic approach is the same for other analytics platforms or similar use cases that require custom JavaScript.

1.  In the `plugins` directory, create a directory named `com.example.html5-javascript`.

2.  In the new `com.example.html5-javascript` directory, create a plug-in configuration file \(`plugin.xml`\) that declares the new html5-javascript transformation and its dependencies.

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <?xml-model href="https://www.dita-ot.org/rng/plugin.rnc" type="application/relax-ng-compact-syntax"?>
    
    <plugin id="com.example.html5-javascript">
      <require plugin="org.dita.html5"/>
      <transtype name="html5-javascript" extends="html5" desc="HTML5 with embedded JavaScript"/>
      <feature extension="ant.import" file="build_html5-javascript.xml"/>
    </plugin>
    ```

    **Note:** This plug-in will extend the default HTML5 transformation, so the `<require>` element explicitly defines `org.dita.html5` as a dependency.

3.  In the `com.example.html5-javascript` directory, create a subdirectory named `include`.

4.  In the new `include` subdirectory, create a file named `javascript.ftr.xml` with your custom JavaScript code.

    ```
    <div>
    <!-- Google Analytics -->
    <script>
    console.log('Adding Google Analytics tracker');
    
    (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
    (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
    m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
    })(window,document,'script','https://www.google-analytics.com/analytics.js','ga');
    
    ga('create', 'UA-XXXXX-Y', 'auto');
    ga('send', 'pageview');
    </script>
    <!-- End Google Analytics -->
    </div>
    ```

    The division wrapper will be discarded when generating HTML files, and the contents will be inserted into the `<footer>` element of each page.

    The file contents must be well-formed XML. If your JavaScript snippets include attributes without values \(such as the `async` script attribute\), use valid XML syntax to define the empty attribute:

    Instead of:

    ```
    <script>
      <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
    </script>
    ```

    use:

    ```
    <script>
      <script id="MathJax-script" **async=""** src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
    </script>
    ```

5.  In the `com.example.html5-javascript` root directory, add an Ant script \(`build_html5-javascript.xml`\) to define the transformation type and set the path to the JavaScript footer file created in the previous step.

    ```
    <?xml version='1.0' encoding='UTF-8'?>
    
    <project>
      <target name="dita2html5-javascript"
           depends="dita2html5-javascript.init,
                    dita2html5"/>
      <target name="dita2html5-javascript.init">
        <property name="args.ftr"
              location="${dita.plugin.com.example.html5-javascript.dir}/include/javascript.ftr.xml"/>
      </target>
    </project>
    ```

    **Note:** When defining the path to the footer file from the Ant script, use the plug-in directory property with the *plugin-id* as shown in the example above: `${dita.plugin.*plugin-id*.dir}`.


**Tip:** The files for this sample plug-in are included in the DITA-OT installation directory under `docsrc/samples/plugins/com.example.html5-javascript/` and on [GitHub](https://github.com/dita-ot/docs/tree/develop/samples/plugins/com.example.html5-javascript).

The plug-in directory has the following layout and files:

```
com.example.html5-javascript
├── build_html5-javascript.xml
├── include
│   └── javascript.ftr.xml
└── plugin.xml
```

1.  Use the `dita install` subcommand to install the plug-in.

    **Note:** For more information, see [Installing plug-ins](plugins-installing.md).

2.  Build output with the new transformation type to verify that the plug-in works as intended.

    ```
    ``dita`` **--input**=*my.ditamap* **--format**=html5-javascript
    ```

3.  Open one of the generated HTML topic files in a modern web browser and check the JavaScript **Console**. When the page is loaded, `Adding Google Analytics tracker` will appear on the console to verify that the sample script is loaded.
4.  Remove the `console.log` debugging message from the sample JavaScript code, and replace the `'UA-XXXXX-Y'` placeholder string with the tracking ID of the Google Analytics property you wish to track.

**Tip:** This example places the JavaScript code in the page footer to ensure that page display is not delayed while the script is loaded. If your JavaScript code supports pre-loading and your application targets modern browsers that recognize the `async` script attribute, you may prefer to insert the JavaScript snippet in the `<head>` element of the generated HTML files using the **args.hdf** parameter instead.

**Related information**  


[HTML-based output parameters](../parameters/parameters-base-html.md)

