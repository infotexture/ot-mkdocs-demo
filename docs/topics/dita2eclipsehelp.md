# Eclipse help

The eclipsehelp transformation generates XHTML output, CSS files, and the control files that are needed for Eclipse help.

In addition to the XHTML output and CSS files, this transformation returns the following files, where mapname is the name of the root map.

|File name|Description|
|---------|-----------|
|plugin.xml|Control file for the Eclipse plug-in|
|mapname.xml|Table of contents|
|index.xml|Index file|
|plugin.properties| |
|META-INF/MANIFEST.MF| |

To run the Eclipse help transformation, set the transtype parameter to eclipsehelp, or pass the --format=eclipsehelp option to the dita command line.

```
dita --input=input-file --format=eclipsehelp
```

where:

-   input-file is the DITA map or DITA file that you want to process.

**Related information**  


[Publishing DITA Content Re-Used in Different Context in EPUB and Eclipse Infocenter by Using DITA-OT](https://www.oxygenxml.com/events/2014/dita-ot_day.html#Publishing_DITA_content_re-used_in_different_context)

[Common parameters](../parameters/parameters-base.md)

[HTML-based output parameters](../parameters/parameters-base-html.md)

[Eclipse Help parameters](../parameters/parameters-eclipsehelp.md)

[Handling content outside the map directory](../parameters/generate-copy-outer.md)

[Official Eclipse website](http://www.eclipse.org)

