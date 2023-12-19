# XSLT-parameter extension points

You can use these extension points to pass parameters into existing XSLT steps in both the pre-processing pipeline and DITA-OT transformation. The parameters generally will be available as global `<xsl:param>` values with XSLT overrides.

## Pre-processing

You can use the following extension points to pass parameters to modules in the pre-processing pipeline:

-   **__dita.preprocess.conref.param__**

    Pass parameters to the `conref` module in the pre-processing pipeline

-   **__dita.preprocess.mappull.param__**

    Pass parameters to the `mappull` module in the pre-processing pipeline

-   **__dita.preprocess.mapref.param__**

    Pass parameters to the `mapref` module in the pre-processing pipeline

-   **__dita.preprocess.topicpull.param__**

    Pass parameters to the `topicpull` module in the pre-processing pipeline


## Transformations

You can use the following extension points to pass parameters to modules in DITA-OT transformations:

-   **__dita.conductor.eclipse.toc.param__**

    Pass parameters to the XSLT step that generates the Eclipse Help table of contents \(TOC\).

-   **__dita.conductor.html.param__**

    Pass parameters to the HTML and HTML Help transformations.

-   **__dita.conductor.html5.param__**

    Pass parameters to the HTML5 transformation.

-   **__dita.conductor.html5.toc.param__**

    Pass parameters to the XSLT step that generates the HTML5 table of contents \(TOC\).

-   **__dita.conductor.pdf2.param__**

    Pass parameters to the PDF transformation.

-   **__dita.conductor.xhtml.param__**

    Pass parameters to the XHTML and Eclipse Help transformations.

-   **__dita.conductor.xhtml.toc.param__**

    Pass parameters to the XSLT step that generates the XHTML table of contents \(TOC\).


## Example

The following two files represent a complete \(albeit simple\) plug-in that passes the parameters defined in the `insertParameters.xml` file to the XHTML transformation process.

```
<plugin id="com.example.newparam">
  <feature extension="dita.conductor.xhtml.param"
           file="insertParameters.xml"/>
</plugin>
```

```
<dummy xmlns:if="ant:if" xmlns:unless="ant:unless">
  *&lt;!-- Any Ant code allowed in xslt task is possible. Example: --&gt;*
  <param name="paramNameinXSLT" expression="${antProperty}"
         if:set="antProperty"/>
</dummy>
```

