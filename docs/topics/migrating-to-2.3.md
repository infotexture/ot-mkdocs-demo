# Migrating to release 2.3

In DITA-OT 2.3, HTML5 table processing has been refactored to use HTML5 best practices and improved CSS properties. In PDF output, table heads and key columns no longer include shading, and unused localization variables have been deprecated. The template for generated error messages has been updated to use a single `id` variable that contains the entire message ID.

**Note:** This topic provides a summary of changes in DITA-OT 2.3 that may require modifications to custom stylesheets or plug-ins. For more information on changes in this release, see the [DITA-OT 2.3 Release Notes](https://www.dita-ot.org/2.3/release-notes/).

## HTML5

The HTML5 table processing has been refactored to use valid HTML5 markup, HTML5 best practices, and better CSS properties for styling. [BEM](https://en.bem.info/methodology/)-style CSS classes are now generated with the name of the containing element, the name of the attribute, and the value of the attribute.

Common CSS files are now generated using separate modules for each DITA domain, implemented as [Sass](http://sass-lang.com) partials to better support extensions with CSS frameworks, custom plug-ins and future toolkit versions.

## HTML-based formats

The XSLT `tm-area` named template, which used to toggle rendering of trademark symbols in US English and Asian languages \(Japanese, Korean, and both Chinese\) but ignore them in all other languages, has been deprecated. Trademark symbols are now rendered uniformly for all languages and the template will be removed in an upcoming release.

In previous releases, short descriptions in `abstract` elements were rendered as division elements \(`div`\), rather than paragraphs \(`p`\). Processing has been revised to ensure that short descriptions are consistently rendered as paragraphs, regardless of whether they appear in `abstract` elements. Users who have previously implemented custom CSS rules to style `div.shortdesc` like paragraphs should be able to remove these rules.

## PDF

The `antiquewhite` background color has been removed from table heads and key column contents in `simpletable` and `properties` tables to synchronize presentation with `choicetable` and provide a more uniform customization baseline between PDF output and HTML-based formats.

PDF: The I18N Java and XSLT processing code has been merged into single task. This eliminated the need for a stage3.fo file in the temporary directory; instead, topic.fo is generated directly from stage2.fo. If custom plug-ins were implemented to handle stage3.fo, they would need to be updated.

Localization variables that are no longer used in PDF processing have been deprecated and will be removed in an upcoming release. PDF customization plug-ins that make use of these variables should plan to refactor accordingly:

-   Back button title
-   Contents button title
-   Forward button title
-   Index button title
-   Index multiple entries separator
-   Main page button title
-   Next page button title
-   Online help prefix
-   Online Help Search Method And
-   Online Help Search Method Field
-   Online Help Search Method Or
-   Previous page button title
-   Search button title
-   Search Case Sensitive Switch
-   Search Excluded Stop Words Message
-   Search Highlight Switch
-   Search index button title
-   Search index field title
-   Search index next button title
-   Search Search Give No Results Message
-   Search Search in Progress Message
-   Search Stopped Message
-   Search text button title
-   Search text field title
-   Search title
-   Search Whole Words Switch
-   Untitled section

**Note:** Most of these variables were never used by the PDF process, and most were not supported \(or localized\) for any language other than English.

## Deprecated properties and targets

The following Ant properties have been deprecated:

-   conreffile

The following preprocessing targets have been deprecated:

-   conref-check
-   coderef

## Pre-processing

The order of the `chunk` and `move-meta-entries` pre-processing stages has been switched so that `chunk` comes first. This ensures that metadata is properly pulled or pushed into the chunked version of DITA topics.

## Generating error messages

Previously, the XSLT `output-message` named template for generating error messages combined a global `msgprefix` variable and two parameters to determine the actual message ID. This function has been updated to use a single `id` variable that contains the entire message ID.

Plug-ins that make use of the `output-message` function should be updated to use the single `id` variable, as in:

```
<xsl:call-template name="output-message">
  <xsl:with-param name="id" select="'FULLMESSAGENUMBER'"/>
  <xsl:with-param name="msgparams">optional-message-parameters</xsl:with-param>
</xsl:call-template>
```

The `msgprefix` XSL variable \(“DOTX”\) has been deprecated and will be removed in an upcoming release.

