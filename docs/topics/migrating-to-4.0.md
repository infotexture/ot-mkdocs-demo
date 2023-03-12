# Migrating to release 4.0

DITA-OT 4.0 requires Java 17 and includes a new plug-in for easier PDF customization, project file improvements, updates to LwDITA processing, and support for the split chunking feature in the latest draft of the upcoming DITA 2.0 standard.

**Note:** This topic provides a summary of changes in DITA-OT 4.0 that may require modifications to custom stylesheets or plug-ins. For more information on changes in this release, see the [DITA-OT 4.0 Release Notes](https://www.dita-ot.org/4.0/release-notes/).

## DITA-OT now requires Java 17

DITA-OT 4.0 is designed to run on Java version 17 or later and built and tested with the Open Java Development Kit \(OpenJDK\). Compatible Java distributions are available from multiple sources:

-   You can download the Oracle JRE or JDK from [oracle.com/java](https://www.oracle.com/java/technologies/downloads/) under commercial license.
-   Eclipse Temurin is the free OpenJDK distribution available from [adoptium.net](https://adoptium.net/temurin/releases/?version=17).
-   Free OpenJDK distributions are also provided by [Amazon Corretto](https://aws.amazon.com/corretto/), [Azul Zulu](https://www.azul.com/downloads/), and [Red Hat](https://developers.redhat.com/products/openjdk/download).

**Note:** The Java virtual machine is generally backwards compatible, so class files built with earlier versions should still run correctly with Java 17 and DITA-OT 4.0. If your DITA-OT installation contains plug-ins with custom Java code, you may need to recompile these with Java 17 — but in most cases, this step should not be necessary.

## Deprecated attribute set reflection in PDF2

The legacy attribute set reflection in PDF2 has been replaced with code that generates new attribute sets directly. This change is backwards-compatible as the old attribute set reflection code has been retained, but PDF2 now uses the new attribute set generation mechanism everywhere reflection was used. Custom plug-ins that still use reflection should be updated to the new approach, as the legacy code may be removed in a future version. [\#3827](https://github.com/dita-ot/dita-ot/issues/3827), [\#3829](https://github.com/dita-ot/dita-ot/issues/3829)

## Code references now default to UTF-8 encoding

The default character set for code references has been changed from the system default encoding to UTF-8.

This allows a wider range of characters to be used without needing to specify the `@format` attribute on the `coderef` element as described in [character set definition](../reference/extended-functionality.md#coderef-charset) or change the default encoding in the [configuration.properties file](../parameters/configuration-properties-file.md). [\#4046](https://github.com/dita-ot/dita-ot/issues/4046)

**Note:** If you have code references that require a different encoding, use either of these mechanisms to specify the character set explicitly.

## Deprecated `place-tbl-lbl` template in HTML5

The `place-tbl-lbl` template that was originally used to define table titles in XHTML has been deprecated in HTML5 processing and will be removed in a future release. This template was carried over from XHTML code \(which still has a copy that is used\), but the copy in HTML5 is not called. [\#3435](https://github.com/dita-ot/dita-ot/issues/3435), [\#4056](https://github.com/dita-ot/dita-ot/issues/4056)

