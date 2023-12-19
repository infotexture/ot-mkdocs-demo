# XHTML

The xhtml transformation generates XHTML output and a table of contents \(TOC\) file. This was the first transformation created for DITA Open Toolkit, and originally served as the basis for all HTML-based transformations.

The XHTML output is always associated with the default DITA-OT CSS file \(`commonltr.css` or `commonrtl.css` for right-to-left languages\). You can use toolkit parameters to add a custom style sheet to override the default styles.

To run the XHTML transformation, set the **transtype** parameter to xhtml, or pass the **--format**=xhtml option to the `dita` command line.

```
``dita`` **--input**=*input-file* **--format**=xhtml
```

where:

-   *input-file* is the DITA map or DITA file that you want to process.

**Related information**  


[Setting parameters for custom HTML](../topics/html-customization-parameters.md)

[Common parameters](../parameters/parameters-base.md)

[HTML-based output parameters](../parameters/parameters-base-html.md)

[XHTML parameters](../parameters/parameters-xhtml.md)

[Handling content outside the map directory](../parameters/generate-copy-outer.md)

