# Migrating to release 3.2

DITA-OT 3.2 includes new command-line options, support for RELAX NG parsing and validation, preliminary processing for the XDITA authoring format proposed for Lightweight DITA, and a plug-in registry that makes it easier to discover and install new plug-ins.

**Note:** This topic provides a summary of changes in DITA-OT 3.2 that may require modifications to custom stylesheets or plug-ins. For more information on changes in this release, see the [DITA-OT 3.2 Release Notes](https://www.dita-ot.org/3.2/release-notes/).

## Deprecated targets

The configuration-jar Ant target used during the plug-in integration process has been deprecated and may be removed in an upcoming release. This was previously used to package additional configuration files and properties into lib/dost-configuration.jar, but recent versions of DITA-OT include the config directory in the classpath for this purpose, so the configuration JAR is no longer necessary.

## Secure connections to the plug-in registry

**Attention:** To ensure data integrity during the plug-in installation process, Transport Layer Security \(TLS\) will soon be required to access the plug-in registry. If you are using DITA-OT 3.2 or 3.2.1 and are unable to upgrade to the latest version, modify the `registry` key in the config/configuration.properties file to switch the URI schema to `http**s**://`, so the entry reads `https://plugins.dita-ot.org/`.

For more information, see [Adding plug-ins via the registry](plugins-registry.md).

