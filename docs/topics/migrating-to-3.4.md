# Migrating to release 3.4

DITA-OT 3.4 includes an official Docker container image, a separate plug-in for PDF indexing, a new option to skip HTML5 cover pages, and initial support for project files that allow you to define multiple deliverables in advance, and publish them all at once.

**Note:** This topic provides a summary of changes in DITA-OT 3.4 that may require modifications to custom stylesheets or plug-ins. For more information on changes in this release, see the [DITA-OT 3.4 Release Notes](https://www.dita-ot.org/3.4/release-notes/).

## New indexing plug-in

DITA-OT 3.4 extracts the PDF indexing code to a separate org.dita.index plug-in, and adds a new `depend.org.dita.pdf2.index` extension point that can be used to add custom index processing targets to PDF output.

The built-in index processing has been disabled and deprecated. If you have overridden index processing via the `transform.topic2fo` target in the past, you can set the new org.dita.index.skip property to yes and re-enable the `transform.topic2fo.index` target with `feature extension="depend.org.dita.pdf2.index" value="transform.topic2fo.index"/` in your plug-in configuration.

|Plug-in|Source code location|
|-------|--------------------|
|org.dita.index|[https://github.com/dita-ot/org.dita.index](https://github.com/dita-ot/org.dita.index)|

## Legacy plug-ins removed

DITA-OT 3.4 no longer includes the following legacy transformation plug-ins in the default distribution:

|Plug-in|Source code location|
|-------|--------------------|
|TocJS|[https://github.com/dita-ot/com.sophos.tocjs](https://github.com/dita-ot/com.sophos.tocjs)|
|troff|[https://github.com/dita-ot/org.dita.troff](https://github.com/dita-ot/org.dita.troff)|

**Note:** If necessary, legacy plug-ins may be re-installed from earlier DITA-OT distributions, but they are no longer actively maintained or supported by the core toolkit committers. The source code is available on GitHub for anyone interested in maintaining the plug-ins for use with future toolkit versions.

To re-install the plug-in\(s\) from the plug-in registry at [dita-ot.org/plugins](https://www.dita-ot.org/plugins), run the following command\(s\):

```syntax-bash
dita --install=com.sophos.tocjs
dita --install=org.dita.troff
```

