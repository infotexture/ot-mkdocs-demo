# Re-usable components

Warehouse topic used to store re-usable content for concept topics or other constructs that would not be valid in the existing warehouse task `conref-task.dita`.

## Upgrade stylesheets to XSLT 2.0

The Saxon project has announced plans to remove XSLT 1.0 support from the Saxon-HE library that ships with DITA-OT:

> …we’re dropping XSLT 1.0 backwards compatibility mode from Saxon-HE, and hope to eliminate it entirely in due course.

> [**https://www.xml.com/news/release-saxon-98/**](https://www.xml.com/news/release-saxon-98/)

DITA-OT 3.0 and 3.0.1 included Saxon-HE 9.8.0.5, which rejects XSLT stylesheets that specify `version="1.0"`. Plug-ins with XSLT templates specifying version 1.0 will fail with the message “`XSLT 1.0 compatibility mode is not available in this configuration`.”

To resolve this issue, change any occurrences of `<xsl:stylesheet version="1.0">` in custom plug-in stylesheets to at least `<xsl:stylesheet version="2.0">`.

**Tip:** DITA-OT 3.0.2 includes Saxon-HE 9.8.0.7, which restores XSLT 1.0 backwards-compatibility mode, but the DITA Open Toolkit project recommends upgrading all stylesheets to XSLT 2.0 to ensure plug-ins remain compatible with future versions of DITA-OT and Saxon-HE.

## Validating plug-ins

DITA-OT includes a RELAX NG schema file that can be used to validate the `plugin.xml` files that define the capabilities of each plug-in.

To ensure the syntax of your custom plug-in is correct, include an `xml-model` processing instruction at the beginning of the `plugin.xml` file, immediately after the XML prolog:

`xml-model href="https://www.dita-ot.org/rng/plugin.rnc" type="application/relax-ng-compact-syntax"`

If your authoring environment does not apply this schema automatically, point your editor to `*dita-ot-dir*/resources/plugin.rnc` to associate the schema with your plug-in file.

## **DITA for Print: A DITA Open Toolkit Workbook** \(Second Edition, 2017\)

Authored by Leigh W. White, DITA Specialist at IXIASOFT, and published by XML Press, **DITA for Print** walks readers through developing a PDF customization from scratch.

Here is an excerpt from the back cover:

> **DITA for Print** is for anyone who wants to learn how to create PDFs using the DITA Open Toolkit without learning everything there is to know about XSL-FO, XSLT, or XPath, or even about the DITA Open Toolkit itself. **DITA for Print** is written for non-programmers, by a non-programmer, and although it is written for people who have a good understanding of the DITA standard, you don’t need a technical background to get custom PDFs up and running quickly.

This is an excellent, long-needed resource that was initially developed in 2013 for DITA-OT 1.8.

The second edition has been revised to cover DITA Open Toolkit Version 2, including customizing the DITA 1.3 troubleshooting topic type, localization strings, bookmarks, and the new back-cover functionality.

**Important:**

The first edition of **DITA for Print** recommended copying entire files from the PDF2 plug-in to your custom plug-in. The DITA-OT project — and the second edition of the book — do not recommend this practice.

Instead, you should copy only the specific attribute sets and templates that you want to override. Following this practice will more cleanly isolate your customizations from the DITA-OT code, which will make it easier for you to update your plug-ins to work with future versions of DITA-OT.

## **DITA for Practitioners: Volume 1, Architecture and Technology** \(2012\)

Authored by Eliot Kimber and published by XML Press, this seminal resource contains a chapter dedicated to DITA Open Toolkit: “Running, Configuring, and Customizing the Open Toolkit”. In addition to a robust overview of DITA-OT customization and extension, the chapter contains a detailed example of customizing a PDF plug-in to specify 7" × 10" paper size and custom fonts for body text and headers.

The DITA-OT chapter in **DITA for Practitioners: Volume 1** was written for DITA-OT 1.5.4, which was the latest stable version at the time it was written.

## Supported Java versions

DITA-OT 4.1 is designed to run on Java version 17 or later and built and tested with the Open Java Development Kit \(OpenJDK\). Compatible Java distributions are available from multiple sources:

-   You can download the Oracle JRE or JDK from [oracle.com/java](https://www.oracle.com/java/technologies/downloads/) under commercial license.
-   Eclipse Temurin is the free OpenJDK distribution available from [adoptium.net](https://adoptium.net/temurin/releases/?version=17).
-   Free OpenJDK distributions are also provided by [Amazon Corretto](https://aws.amazon.com/corretto/), [Azul Zulu](https://www.azul.com/downloads/), and [Red Hat](https://developers.redhat.com/products/openjdk/download).

**Note:** The Java virtual machine is generally backwards compatible, so class files built with earlier versions should still run correctly with Java 17 and DITA-OT 4.1. If your DITA-OT installation contains plug-ins with custom Java code, you may need to recompile these with Java 17 — but in most cases, this step should not be necessary.

## Limitations of map-first pre-processing

The internal extension points that run before or after individual steps in the original `preprocess` pipeline \(`preprocess.*.pre/preprocess.*.post`\) are not available in the newer map-first preprocessing pipeline \(`preprocess2`\), which is used in the PDF and HTML Help transformations as of DITA-OT 3.0.

## Unbundled plug-ins

**Note:** If necessary, legacy plug-ins may be re-installed from earlier DITA-OT distributions, but they are no longer actively maintained or supported by the core toolkit committers. The source code is available on GitHub for anyone interested in maintaining the plug-ins for use with future toolkit versions.

## New subcommands in 3.5

-   **`dita deliverables`**

    Prints the list of deliverables in a project *file*

-   **`dita install`**

    Installs or reloads plug-ins \(replaces `dita` **--install**\)

-   **`dita plugins`**

    Prints a list of installed plug-ins \(replaces `dita` **--plugins**\)

-   **`dita transtypes`**

    Prints a list of installed transformation types, or *output formats* \(replaces `dita` **--transtypes**\)

-   **`dita uninstall`**

    Removes and deletes a plug-in \(replaces `dita` **--uninstall**\)

-   **`dita version`**

    Prints version information and exits \(replaces `dita` **--version**\)


## Recommendations for upgrading DITA-OT customizations

When migrating customizations, identify the version of the toolkit you're currently using \(base version\) and the version of the toolkit you want to migrate to \(target version\). Then, review all of the migration changes described in *all* of the versions from the base through the target. For instance, if you're currently on 2.2 and want to move to 3.3, you should review all of the changes in 2.3 through 3.3. You may want to start at the oldest version and read forward so you can chronologically follow the changes, since it is possible that files or topics have had multiple changes.

## Common format for generated text

Prior to DITA-OT 3.7, there were two different XML structures for adding or modifying generated text \(gentext\). The base plug-in **org.dita.base** and any custom overrides defined via the **dita.strings.xsl** extension point used a root element `<strings>`, with individual strings in `<str>` elements with `@name` attributes. This format was previously used for HTML, and all other output formats except PDF.

```
<?xml version="1.0" encoding="utf-8"?>
<strings xml:lang="en-US">
  <str name="String1">English generated text</str>
</strings>
```

The PDF plug-in **org.dita.pdf2** used a root element `<vars>` with an XML namespace, and strings in `<variable>` elements with `@id` attributes.

```
<?xml version="1.0" encoding="UTF-8"?>
<vars xmlns="http://www.idiominc.com/opentopic/vars">
  <variable id="String1">English generated text</variable>
</vars>
```

Starting with DITA-OT 3.7, these structures have been deprecated and replaced with a new unified format. All files now use `<variables>` as the root element, with the `<variable>` elements previously used in PDF strings. The new format supports the XSL parameters used by the earlier PDF strings format to pass dynamic information such as chapter numbers or figure titles.

```
<?xml version="1.0" encoding="UTF-8"?>
<variables>
  <variable id="String1">English generated text</variable>
</variables>
```

The old formats are still supported, but plug-in developers should update any generated text files to reflect the new structure, as support for the old formats may be removed in a future release. [\#3817](https://github.com/dita-ot/dita-ot/issues/3817)

**Tip:** For details on the differences in [Markdown formats](../reference/markdown-formats.md), see [Markdown DITA syntax](../reference/markdown/Markdown-DITA-syntax.md), [MDITA syntax](../reference/markdown/MDITA-syntax.md), and [Format comparison](../reference/markdown/Format-comparison.md).

