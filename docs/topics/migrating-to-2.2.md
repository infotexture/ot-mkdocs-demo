# Migrating to release 2.2

In DITA-OT 2.2, the HTML5 transformation was refactored as its own plug-in and separate plug-ins were created for each of the rendering engine-specific PDF transformations.

**Note:** This topic provides a summary of changes in DITA-OT 2.2 that may require modifications to custom stylesheets or plug-ins. For more information on changes in this release, see the [DITA-OT 2.2 Release Notes](https://www.dita-ot.org/2.2/release-notes/).

## HTML5

The HTML5 transformation introduced in release 2.0 as part of the XHTML plug-in has been moved to a separate HTML5 plug-in. Customizations that extended the previous HTML5 output under the XHTML plug-in will probably need to be refactored on the new HTML5 plug-in.

Note title processing has been revised to use a common `note__title` class for note elements of all types. The legacy `\{$type\}title` classes \(such as `.notetitle`, `.cautiontitle`, `.tiptitle`, etc.\) are included for backwards compatibility, but are deprecated and will be removed in an upcoming release. Stylesheets that apply formatting overrides to note titles should be revised to replace the deprecated class selectors with the equivalent descendant selectors, for example `.note_note .note__title`, `.note_caution .note__title`, `.note_tip .note__title`, etc.

## PDF

Processing specific to Apache FOP, Antenna House Formatter, and RenderX XEP has been separated into separate plug-ins for each of those rendering engines. Customizations that extended this processing might need to extend the new `org.dita.pdf2.fop`, `org.dita.pdf2.axf`, or `org.dita.pdf2.xep` plug-ins.

PDF customizations that are not specific to a rendering engine can continue to extend the `org.dita.pdf2` plug-in as before.

The default format for page numbers in the table of contents \(`toc`\) was switched to roman to align with `preface` and ensure consistent numbering styles for all `frontmatter` components in `bookmap`. This prevents numbering from switching back and forth between styles in bookmaps where the Preface follows the table of contents. Earlier versions of DITA-OT produced numbering sequences like `1,2,3,4,v,vi,7,8` in this use case.

## Deprecated properties

The following Ant properties have been deprecated:

-   user.input.file, use user.input.file.uri instead to specify the input file system path
-   user.input.dir, use user.input.dir.uri instead to specify the input directory system path
-   InputMapDir, use InputMapDir.uri instead to specify the input map directory system path

