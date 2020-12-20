# Migrating to release 2.5

In DITA-OT 2.5, several frequently-overridden legacy style settings were removed from the default PDF plug-in. A separate plug-in can be used to restore the original settings.

**Note:** This topic provides a summary of changes in DITA-OT 2.5 that may require modifications to custom stylesheets or plug-ins. For more information on changes in this release, see the [DITA-OT 2.5 Release Notes](https://www.dita-ot.org/2.5/release-notes/).

## Deprecated logging parameters

The `args.debug` and `args.logdir` properties have been deprecated and will be removed in an upcoming version of DITA-OT.

-   To enable debug logging, use dita --debug.

    **Attention:** Debug logging requires additional resources and can slow down the build process, so it should only be enabled when further details are required to diagnose problems.

-   To write the log to a file, use dita --logfile=file or ant -l file and specify the path to the log file.

    Unless an absolute path is specified, the value will be interpreted relative to the current directory.


## Default PDF style improvements

Several legacy styles have been modified or removed in the default PDF plug-in `org.dita.pdf2`, including the following:

-   In task topics with only a single step, the step is now rendered as a simple block \(rather than as a list item without a label\).
-   Table containers now inherit the initial indentation \(`start-indent`\) from the parent elements.
-   Borders and indentation have been removed from `example` elements.
-   Links are no longer italicized.
-   Titles for related link lists have been standardized to use the `common.title` attribute set \(which applies the `sans-serif` font-family\) and bold font weight.
-   Several remaining occurrences of left/right borders, margins, padding, and text alignment now use the corresponding start/end equivalents to better support right-to-left languages.

## External plug-in for legacy PDF styling

If you have a custom PDF plug-in that explicitly depends on the previous default settings for the aforementioned styles, the `org.dita.pdf2.legacy` plug-in can be used to restore the pre–2.5 styles.

|Plug-in|Source code location|
|-------|--------------------|
|`org.dita.pdf2.legacy`|[https://github.com/dita-ot/org.dita.pdf2.legacy](https://github.com/dita-ot/org.dita.pdf2.legacy)|

To install the legacy PDF plug-in, run the following command:

```
dita --install=https://github.com/dita-ot/org.dita.pdf2.legacy/archive/2.5.zip
```

**Attention:** Only install the legacy PDF plug-in if you have a custom PDF plug-in that requires the pre–2.5 styles. If your plug-in was designed for DITA-OT 2.4 and does not override these settings, there is no need to install the legacy PDF plug-in.

