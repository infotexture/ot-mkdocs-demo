# Internationalization configuration

The fo/i18n folder houses custom internationalization files that override the standard configurations in org.dita.pdf2/cfg/fo/i18n.

As with index configuration and variable overrides, each file contains data for a single language, and should take that language’s ISO 639-1 language designator as its name.

Each configuration file contains mappings of certain symbols to the Unicode codepoint which should be used to represent them in the given locale.

The best way to start editing a custom configuration is by making a copy of the original from org.dita.pdf2/cfg/fo/i18n and making changes as desired.

In order to apply a custom configuration to your publishing outputs, edit catalog.xml and uncomment the appropriate entry in the “I18N configuration override entries” section.

