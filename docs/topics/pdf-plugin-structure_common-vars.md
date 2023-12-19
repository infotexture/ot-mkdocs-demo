# Variable overrides

The `common/vars` folder houses custom variable definitions that override the standard definitions in `org.dita.pdf2/cfg/common/vars`.

As with index configuration, each file contains data for a single language, and should take that language’s ISO 639-1 language designator as its name.

Variable files contain a set of `<variable>` elements, identified by their `@id` attribute. The variable definitions are used to store static text that is used as part of the published outputs. For example, page headers, hyperlinks, etc. The id attribute for each variable should make it clear how the variable text is being used.

Some variables contain `<param>` elements which indicate parameter values that are substituted at publish time by the XSL. For example, a page number that is being generated as part of the publishing process might be identified by `<param ref-name="number"/>` When editing or translating a variable file, these should be included in the translation, though they can be moved and rearranged within the `<variable>` content as needed.

The best way to start editing a custom variables file is by making a copy of the original from `org.dita.pdf2/cfg/common/vars` and making changes as desired. When adding a new language, start from an existing language’s list of variables and translate each entry as needed.

Note that unchanged `<variable>` elements can be omitted: the custom variables file need only include those `<variable>` elements which you have modified. Variables not found in the custom file will are taken from the standard variable files.

Applying a custom variable does not require modifying the `catalog.xml` file. The publishing process will automatically use any custom variables definitions in place of the original ones.

**Related information**  


[How to add or modify generated text strings](../topics/plugin-addgeneratedtext.md)

