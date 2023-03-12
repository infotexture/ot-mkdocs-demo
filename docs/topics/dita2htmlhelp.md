# HTML Help

The htmlhelp transformation generates HTML output, CSS files, and the control files that are needed to produce a Microsoft Compiled HTML Help \(.chm\) file.

In addition to the HTML output and CSS files, this transformation returns the following files, where mapname is the name of the root map.

|File name|Description|
|---------|-----------|
|mapname.hhc|Table of contents|
|mapname.hhk|Sorted index|
|mapname.hhp|HTML Help project file|
|mapname.chm|Compiled HTML Help file

 **Note:** The compiled file is only generated if the HTML Help Workshop is installed on the build system.

|

To run the HTML Help transformation, set the transtype parameter to htmlhelp, or pass the --format=htmlhelp option to the dita command line.

```
dita --input=input-file --format=htmlhelp
```

where:

-   input-file is the DITA map or DITA file that you want to process.

**Related information**  


[Common parameters](../parameters/parameters-base.md)

[HTML-based output parameters](../parameters/parameters-base-html.md)

[Microsoft Compiled HTML Help parameters](../parameters/parameters-htmlhelp.md)

[Handling content outside the map directory](../parameters/generate-copy-outer.md)

