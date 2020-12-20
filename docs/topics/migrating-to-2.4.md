# Migrating to release 2.4

In DITA-OT 2.4, the HTML5 transformation was refactored as an independent plug-in that no longer depends on the XHTML plug-in.

**Note:** This topic provides a summary of changes in DITA-OT 2.4 that may require modifications to custom stylesheets or plug-ins. For more information on changes in this release, see the [DITA-OT 2.4 Release Notes](https://www.dita-ot.org/2.4/release-notes/).

## HTML5

-   The HTML5 transformation introduced in release 2.0 as part of the XHTML plug-in was moved to a separate HTML5 plug-in in release 2.2, but that version of the HTML5 transformation still depended on the XHTML plug-in for certain common processing.

In release 2.4, all dependencies between HTML5 and XHTML have been removed to ensure that HTML5 processing can be further refactored in the future without affecting XHTML output, or other HTML-based transformations such as eclipsehelp, htmlhelp or javahelp.

    Customizations that extended the previous HTML5 output under the XHTML plug-in \(as provided in releases 2.0 and 2.1\) or the HTML5 plug-in that shipped with release 2.2 will need to be refactored to build on the new HTML5 plug-in.

-   Note title processing was revised in release 2.2 to include a common `note__title` class for note elements of all types. The legacy `\{$type\}title` classes \(such as `.notetitle`, `.cautiontitle`, `.tiptitle`, etc.\) were included in release 2.2 for backwards compatibility, but have now been removed in release 2.4.

    Stylesheets that apply formatting overrides to note titles should be revised to replace the deprecated class selectors with the equivalent descendant selectors, for example:

    -   `.note_note .note__title`
    -   `.note_caution .note__title`
    -   `.note_tip .note__title`

## Legacy plug-ins removed

DITA-OT 2.4 no longer includes the following legacy transformation plug-ins in the default distribution:

|Plug-in|Source code location|
|-------|--------------------|
|DocBook|[https://github.com/dita-ot/org.dita.docbook](https://github.com/dita-ot/org.dita.docbook)|
|Eclipse Content|[https://github.com/dita-ot/org.dita.eclipsecontent](https://github.com/dita-ot/org.dita.eclipsecontent)|
|OpenDocument Text|[https://github.com/dita-ot/org.dita.odt](https://github.com/dita-ot/org.dita.odt)|
|Word RTF|[https://github.com/dita-ot/org.dita.wordrtf](https://github.com/dita-ot/org.dita.wordrtf)|

**Note:** If necessary, legacy plug-ins may be re-installed from earlier DITA-OT distributions, but they are no longer actively maintained or supported by the core toolkit committers. The source code is available on GitHub for anyone interested in maintaining the plug-ins for use with future toolkit versions.

