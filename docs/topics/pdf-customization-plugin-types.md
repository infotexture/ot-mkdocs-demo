# Types of custom PDF plug-ins

There are two common types of plug-ins: A plug-in that simply sets the DITA-OT parameters to be used when a PDF is generated, and a plug-in that overrides aspects of the base DITA-OT PDF transformation. A plug-in can, of course, do both of these things.

## Plug-in that only provides DITA-OT parameters

You might want to build a transformation type that uses a transformation as-is; however, you might want to ensure that certain DITA-OT parameters are used. For an example of this approach, see [Setting parameters with plug-ins](plugin-set-parameters.md).

## Plug-in that overrides the base PDF transformation

Production uses of DITA-OT typically rely on a custom PDF plug-in to render PDFs that are styled to match corporate or organizational guidelines. Such customization plug-ins often override the following aspects of DITA-OT default output:

-   Generated text strings
-   XSL templates
-   XSL-FO attribute sets

