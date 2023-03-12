# The configuration.properties file

The configuration.properties file controls certain common properties, as well as some properties that control PDF processing.

The contents of the config/configuration.properties file are added to the DITA-OT configuration in the `dost-configuration.jar` file when the plug-in integration process runs. The following properties are typically set in this file:

-   **default.cascade**

    Specifies the processing default value for the DITA 1.3 `@cascade` attribute, which determines how map-level metadata attributes are applied to the children of elements where the attributes are specified. DITA-OT uses the merge value by default for backwards compatibility with DITA 1.2 and earlier.

    **Warning:** This property can only be set in configuration.properties and should not be modified.

-   **temp-file-name-scheme**

    This setting specifies the name of the Java class that defines how the source URL of a topic is mapped to the URL of the temporary file name. The current default method uses a 1:1 mapping, though future implementations may use alternative approaches such as hashes or full absolute paths as file names.

    **Warning:** This property can only be set in configuration.properties and should not be modified.

-   **filter-attributes**

    Specifies additional attributes to be used for filtering, in addition to those defined in the DITA specification. The value is a comma-separated list of attribute QNames in Clark notation.

    For example, to permit filtering by `@importance` and `@status` attributes, set:

    ```language-properties
    filter-attributes = importance, status
    ```

-   **flag-attributes**

    Specifies additional attributes to be used for flagging, in addition to those defined in the DITA specification. The value is a comma-separated list of attribute QNames in Clark notation.

    For example, to enable flagging based on a custom `@cms:review` attribute, set:

    ```language-properties
    flag-attributes = {http://www.cms.com/}review
    ```

    With this setting, a DITAVAL file could be used to flag content marked as `new` with a purple background:

    ```language-xml
    <val xmlns:cms="http://www.cms.com/">
      <prop action="flag" att="cms:review" val="new" backcolor="purple"/>
    </val>
    ```

-   **cli.color**

    Specifies whether the dita command prints colored output on the command line console. When set to true, error messages in dita command output will appear in red on terminals that support [ANSI escape codes](https://en.wikipedia.org/wiki/ANSI_escape_code), such as on Linux or macOS. Set to false to disable the color. \(Colored output is not supported on Windows consoles such as cmd.exe or PowerShell\).

-   **default.coderef-charset**

    Specifies the default character set for code references.

-   **plugindirs**

    A semicolon-separated list of directory paths that DITA-OT searches for plug-ins to install; any relative paths are resolved against the DITA-OT base directory. Any immediate subdirectory that contains a plugin.xml file is installed.

    **Tip:** You can use this property to test custom plug-ins that are stored in other locations. For example, to install all of the sample plug-ins that are included in the DITA-OT documentation, append ;docsrc/samples/plugins to the property value and run dita --install. You can maintain custom plug-ins in version-controlled repositories outside of the DITA-OT installation directory, and add the repository locations to the list of plug-in directories here to test your code.

-   **plugin.ignores**

    A semicolon-separated list of directory names to be ignored during plug-in installation; any relative paths are resolved against the DITA-OT base directory.

-   **plugin.order**

    Defines the order in which plug-ins are processed. In XML catalog files, the order of imports is significant. If multiple plug-ins define the same thing \(differently\), the first catalog entry “wins”. DITA-OT uses this property to define the order in which catalog entries are written. This mechanism is currently used to ensure that DITA 1.3 grammar files take precedence over their DITA 1.2 equivalents.

-   **registry**

    Defines the list \(and order\) of plug-in repositories that are searched for available plug-ins during the installation process. In addition to the main plug-in registry at [dita-ot.org/plugins](https://www.dita-ot.org/plugins), you can create a registry of your own to store the custom plug-ins for your company or organization. To add a new entry, append the URL for your custom registry directory to the `registry` key value, separating each entry with a space. For more information, see [Adding plug-ins via the registry](../topics/plugins-registry.md).

-   **org.dita.pdf2.i18n.enabled**

    Enables internationalization \(I18N\) font processing to provide per-character font selection for FO renderers that do not support the `font-selection-strategy` property \(such as Apache FOP\).

    When this feature is enabled, DITA-OT uses a font mapping process that takes the content language into consideration. The mapping process uses configuration files for each language to define characters that should be rendered with certain logical fonts, and font mappings that associate each logical font to physical font files.

    The following values are allowed:

    -   true \(default\) — Enables font mapping
    -   false — Disables font mapping
    **Tip:** If you don’t use custom character mappings, turning off font mapping makes it easier to define custom fonts simply by changing font names in the XSL attributes files of your custom PDF plug-in. For details, see [Font configuration in PDF2](http://www.elovirta.com/2016/02/18/font-configuration-in-pdf2.html).

-   **default.coderef-charset**

    As of DITA-OT 3.3, the default character set for code references can be changed by specifying one of the character set values supported by the Java [Charset](https://docs.oracle.com/javase/8/docs/api/java/nio/charset/Charset.html) class.


**Related information**  


[Installing plug-ins](../topics/plugins-installing.md)

[DITA 1.3 specification: Cascading of metadata attributes in a DITA map](http://docs.oasis-open.org/dita/dita/v1.3/errata01/os/complete/part1-base/archSpec/base/cascading-in-a-ditamap.html#cascading-in-a-ditamap)

[Example: How the @cascade attribute functions](http://docs.oasis-open.org/dita/dita/v1.3/errata01/os/complete/part1-base/archSpec/base/example-how-cascade-att-functions.html)

[Font configuration in PDF2](http://www.elovirta.com/2016/02/18/font-configuration-in-pdf2.html)

