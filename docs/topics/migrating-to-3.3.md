# Migrating to release 3.3

DITA-OT 3.3 includes new attribute sets for HTML5 customization, support for custom integration processing, rotated table cells in PDF output, and hazard statements in HTML output.

**Note:** This topic provides a summary of changes in DITA-OT 3.3 that may require modifications to custom stylesheets or plug-ins. For more information on changes in this release, see the [DITA-OT 3.3 Release Notes](https://www.dita-ot.org/3.3/release-notes/).

## Secure connections to the plug-in registry

**Attention:** To ensure data integrity during the plug-in installation process, Transport Layer Security \(TLS\) will soon be required to access the plug-in registry. If you are using DITA-OT 3.3, 3.2, or 3.2.1 and are unable to upgrade to the latest version, modify the `registry` key in the `config/configuration.properties` file to switch the URI schema to `http**s**://`, so the entry reads `https://plugins.dita-ot.org/`.

For more information, see [Adding plug-ins via the registry](plugins-registry.md).

## Base plug-in files moved to `plugins` directory

Various XSLT files and other resources have been moved from the root of the DITA-OT installation directory to the base plug-in directory `plugins/org.dita.base`.

**Attention:** There is no longer an `xsl/` directory in the installation root.

If your plug-ins use the `plugin` URI scheme as recommended in the [Plug-in coding conventions](plugin-coding-conventions.md), this change should not require any modifications to custom plug-in code:

> In XSLT, use the `plugin` URI scheme in `<xsl:import>` and `<xsl:include>` to reference files in other plug-ins.

> Instead of:

```language-xml
> <xsl:import href="../../org.dita.base/xsl/common/output-message.xsl"/>
```

> use:

```language-xml
> <xsl:import href="plugin:org.dita.base:xsl/common/output-message.xsl"/>
```

> As with the plug-in directory property in Ant, this allows plug-ins to resolve to the correct directory even when a plug-in moves to a new location. The plug-in is referenced using the syntax `plugin:*plugin-id*:*path/within/plugin/file.xsl*`.

## Relocated catalog

Along with the other base plug-in files, the `catalog-dita.xml` file has been moved from the root of the DITA-OT installation directory to `plugins/org.dita.base`. External systems that rely on this catalog should be updated with the new location. Ant scripts and DITA-OT plug-ins should use the plug-in directory property to refer to the file as `${dita.plugin.org.dita.base.dir}/catalog-dita.xml`. A placeholder with a `<nextCatalog>` entry is provided in the original location for backwards compatibility, but this file may be removed in an upcoming release.

```language-xml
<nextCatalog catalog="plugins/org.dita.base/catalog-dita.xml"/>
```

## Deprecated properties

The `templates` key in configuration properties has been deprecated in favor of the `<template>` element in `plugin.xml`.

## New attribute sets for HTML5 customization

A series of new attribute sets has been added to the default HTML5 transformation to facilitate customization with additional ARIA roles, attributes, or CSS classes. Attribute sets are provided for:

-   `article`
-   `banner`
-   `footer`
-   `main`
-   `navigation`
-   `toc`

If you have previously copied XSL templates \(or template modes\) to custom plug-ins only to add classes required by web frameworks such as Bootstrap or Foundation \(or your company CSS\), you may be able to simplify your customizations by using the new attribute sets instead of overriding the default templates.

