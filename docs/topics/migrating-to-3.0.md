# Migrating to release 3.0

DITA-OT 3.0 adds support for Markdown, normalized DITA output, and the alternative authoring formats proposed for Lightweight DITA. The map-first preprocessing approach provides a modern alternative to the default `preprocess` operation.

**Note:** This topic provides a summary of changes in DITA-OT 3.0 that may require modifications to custom stylesheets or plug-ins. For more information on changes in this release, see the [DITA-OT 3.0 Release Notes](https://www.dita-ot.org/3.0/release-notes/).

## Upgrade stylesheets to XSLT 2.0

The Saxon project has announced plans to remove XSLT 1.0 support from the Saxon-HE library that ships with DITA-OT:

> …we’re dropping XSLT 1.0 backwards compatibility mode from Saxon-HE, and hope to eliminate it entirely in due course.

> [**https://www.xml.com/news/release-saxon-98/**](https://www.xml.com/news/release-saxon-98/)

DITA-OT 3.0 and 3.0.1 included Saxon-HE 9.8.0.5, which rejects XSLT stylesheets that specify `version="1.0"`. Plug-ins with XSLT templates specifying version 1.0 will fail with the message “`XSLT 1.0 compatibility mode is not available in this configuration`.”

To resolve this issue, change any occurrences of `<xsl:stylesheet version="1.0">` in custom plug-in stylesheets to at least `<xsl:stylesheet version="2.0">`.

**Tip:** DITA-OT 3.0.2 includes Saxon-HE 9.8.0.7, which restores XSLT 1.0 backwards-compatibility mode, but the DITA Open Toolkit project recommends upgrading all stylesheets to XSLT 2.0 to ensure plug-ins remain compatible with future versions of DITA-OT and Saxon-HE.

## Legacy plug-ins removed

DITA-OT 3.0 no longer includes the following legacy transformation plug-ins in the default distribution:

|Plug-in|Source code location|
|-------|--------------------|
|JavaHelp|[https://github.com/dita-ot/org.dita.javahelp](https://github.com/dita-ot/org.dita.javahelp)|

**Note:** If necessary, legacy plug-ins may be re-installed from earlier DITA-OT distributions, but they are no longer actively maintained or supported by the core toolkit committers. The source code is available on GitHub for anyone interested in maintaining the plug-ins for use with future toolkit versions.

To re-install the JavaHelp plug-in, run the following command:

```
`dita` **--install**=`https://github.com/dita-ot/org.dita.javahelp/archive/2.5.zip`
```

## Map-first preprocessing

DITA-OT 3.0 provides a map-first preprocessing option as an alternative to the default `preprocess` operation. The method, which was introduced in DITA-OT 2.5 as an experimental feature, has been improved and is ready for use in many production scenarios. Map-first-preprocessing provides the same functionality as the default `preprocess`, but takes a different approach.

The internal extension points that run before or after individual steps in the original `preprocess` pipeline \(`preprocess.*.pre/preprocess.*.post`\) are not available in the newer map-first preprocessing pipeline \(`preprocess2`\), which is used in the PDF and HTML Help transformations as of DITA-OT 3.0.

**Tip:** See [Map-first preprocessing](../reference/map-first-preprocessing.md) for information on how to use \(or test\) map-first preprocessing, or revert to the default `preprocess` target.

## New `ant.import` extension point

A new extension point has been added to make it easier to add new targets to the Ant processing pipeline.

Earlier versions of DITA-OT use the `dita.conductor.target.relative` to call a wrapper file with a dummy task that imports the Ant project file. This approach is still supported for backwards compatibility, but the simpler `ant.import` approach should be used for all new customizations.

**Tip:** See [Adding a new target to the Ant build process](plugin-anttarget.md) for details.

