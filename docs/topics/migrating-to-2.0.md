# Migrating to release 2.0

In DITA-OT 2.0, XSLT templates were converted to XSLT 2.0, variable typing was implemented, and some older templates were refactored or removed. In addition, the `dita` command simplifies distribution of plugins by allowing installation from a URL.

**Note:** This topic provides a summary of changes in DITA-OT 2.0 that may require modifications to custom stylesheets or plug-ins. For more information on changes in this release, see the [DITA-OT 2.0 Release Notes](https://www.dita-ot.org/2.0/readme/changes/rel2.0.html).

## All transformations — variable typing

XSLT stylesheets were converted to XSLT 2.0. With that change, variable types were also implemented. Plug-ins that change template variable values will need to make the following changes:

-   Declare the same types defined in the default templates with `@as`.
-   Ensure that the generated values conform to the declared type.

For example:

```language-xml
<xsl:variable name="urltest">
<xsl:variable name="urltest" **as="xs:boolean"**>
```

## All transformations — refactoring

Much of the toolkit code was refactored for release 2.0. Customization changes that were based on a specific template in a previous version of the toolkit might not work because the modified template is no longer used. If this is the case, the changes will need to be reimplemented based on the new XSLT templates.

## HTML5

A new HTML5 transformation type has been added. Customizations that previously modified the XHTML output to generate valid HTML5 should still work, but basing your customization on the new transformation type might simplify the customization and reduce the work required to maintain compatibility with future versions of the toolkit.

**Note:** The HTML5 transformation was refactored with release 2.2. Before basing your customization on the changes in release 2.0, consider whether you might want to move to release 2.2 instead. See [Migrating to release 2.2](migrating-to-2.2.md).

## Plug-in installation and distribution

Plug-ins can now be installed or uninstalled from a ZIP archive using the new `dita` command. Plug-ins can also be installed from a referenced URL. See [Arguments and options for the dita command](../parameters/dita-command-arguments.md).

