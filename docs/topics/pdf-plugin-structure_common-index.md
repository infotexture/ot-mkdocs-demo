# Index configuration

The common/index folder houses custom index definition files that override the standard definitions in org.dita.pdf2/cfg/common/index.

Each file contains data for a single language, and should take that language’s ISO 639-1 language designator as its name \(for example, pt.xml for Portuguese\). If necessary, locale-specific customizations can be provided by adding a region designator to the file name \(for example, pt\_BR.xml for Brazilian Portuguese\).

The index files consist of `index.group` elements which contain sorting information on one or more characters. Index groups are listed in sort order \(“specials” before numbers, numbers before the letter ‘A‘, etc\), and the `char.set` entries they contain are also listed in sort order \(uppercase before lowercase\).

The best way to start editing a custom index file is by making a copy of the original from org.dita.pdf2/cfg/common/index and making changes as desired.

In order to apply a custom index definition to your publishing outputs, edit catalog.xml and uncomment the appropriate entry in the “Index configuration override entries” section.

**Related information**  


[Custom artwork](../topics/pdf-plugin-structure_common-artwork.md)

[Variable overrides](../topics/pdf-plugin-structure_common-vars.md)

[Custom attributes](../topics/pdf-plugin-structure_fo-attrs.md)

[Internationalization configuration](../topics/pdf-plugin-structure_fo-i18n.md)

[Custom stylesheets](../topics/pdf-plugin-structure_fo-xsl.md)

