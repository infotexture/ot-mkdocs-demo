# Customizing generated text

Generated text is the term for strings that are automatically added by the build process, such as the word **“Note”** before the contents of a `note` element.

-   **`dita.xsl.strings`**

    Add new strings to generated text file.


The generated text extension point is used to add new strings to the default set of generated text from **org.dita.base** for any non-PDF transformation type and from **org.dita.pdf2** for PDF. It also creates the `gentext` element in the intermediate files used by the toolkit. There are several reasons you may want to use the dita.strings.xsl extension point:

-   It can be used to add new text for your own processing extensions; for example, it could be used to add localized versions of the string **“User response”** to aid in rendering troubleshooting information.
-   It can be used to override the default strings in the toolkit; for example, it could be used to reset the English string **“Figure”** to **“Fig.”**
-   It can be used to add support for new languages. For example, it could be used to add support for Vietnamese or Gaelic; it could also be used to support a new variant of a previously supported language, such as Australian English.

If two plug-ins define the same string or add support for the same language using different values, the result will be non-deterministic. In other words, when the same content is processed multiple times, you may get inconsistent generated text results. This is because the toolkit cannot determine which string to use, since more than one match is found. Avoid this possibility by ensuring that only one plug-in defines or overrides string values for each string in each language. Also consider using a naming convention for attributes used to look up the string value by using the ID or purpose of your plug-in.

Generated strings are available to the `getVariable` template used in many DITA-OT XSLT files.

Prior to DITA-OT 3.7, there were two different XML structures for adding or modifying generated text \(gentext\). The base plug-in **org.dita.base** and any custom overrides defined via the dita.strings.xsl extension point used a root element `strings`, with individual strings in `str` elements with `@name` attributes. This format was previously used for HTML, and all other output formats except PDF.

```
<?xml version="1.0" encoding="utf-8"?>
<strings xml:lang="en-US">
  <str name="String1">English generated text</str>
</strings>
```

The PDF plug-in **org.dita.pdf2** used a root element `vars` with an XML namespace, and strings in `variable` elements with `@id` attributes.

```
<?xml version="1.0" encoding="UTF-8"?>
<vars xmlns="http://www.idiominc.com/opentopic/vars">
  <variable id="String1">English generated text</variable>
</vars>
```

Starting with DITA-OT 3.7, these structures have been deprecated and replaced with a new unified format. All files now use `variables` as the root element, with the `variable` elements previously used in PDF strings. The new format supports the XSL parameters used by the earlier PDF strings format to pass dynamic information such as chapter numbers or figure titles.

```
<?xml version="1.0" encoding="UTF-8"?>
<variables>
  <variable id="String1">English generated text</variable>
</variables>
```

The old formats are still supported, but plug-in developers should update any generated text files to reflect the new structure, as support for the old formats may be removed in a future release. [\#3817](https://github.com/dita-ot/dita-ot/issues/3817)

**Related information**  


[Languages supported by the core toolkit](../topics/globalization-languages.md)

[Variable overrides for PDF](../topics/pdf-plugin-structure_common-vars.md)

