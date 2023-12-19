# Overriding strings

Override the default strings in the toolkit when you want to replace an existing string with one of your own; for example, it could be used to reset the English string **“Figure”** to **“Fig.”**

1.  Copy this file to your plug-in.

    -   non-PDF output: `plugins/org.dita.base/xsl/common/strings.xml`
    -   PDF output: `plugins/org.dita.pdf2/cfg/common/vars/strings.xml`
2.  In your plug-in, edit `strings.xml` to contain references to the language files you want to override.

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <!-- Provide strings for my plug-in; this plug-in supports
         English and German. -->
    <langlist>
      <lang xml:lang="en"     filename="strings-en-us.xml"/>
      <lang xml:lang="en-US"  filename="strings-en-us.xml"/>
      <lang xml:lang="de"     filename="strings-de-de.xml"/>
      <lang xml:lang="de-DE"  filename="strings-de-de.xml"/>
    </langlist>
    ```

3.  Copy the language file from you want to override. Paste it into your plug-in's `xsl/common` or `cfg/common/vars` directory.

    Language files are found in:

    -   non-PDF output: `plugins/org.dita.base/xsl/common/`
    -   PDF output: `plugins/org.dita.pdf2/cfg/common/vars/`
4.  Open the language file. Remove all of the variables except those you want to override.

    By removing the variables you will not override, you limit where variables are defined in the toolkit while making your file easier to maintain.

5.  Change the contents of the variable to your desired text.

    Do not modify the `@id` attribute.

    ```
    <variables>
       <variable id="Figure">Fig.</variable>
    </variables>
    ```

6.  Update your `plugin.xml` file to extend the strings available.

    ```
    <plugin id="com.example.your-plugin">
      <feature extension="dita.xsl.strings" file="xsl/common/strings.xml"/>
    </plugin>
    ```

    Your overrides are available to your stylesheets. For example, if processing in a context where the `@xml:lang` value is `en-US`, the following call returns **“Fig.”**, because it was defined as the text for the variable with `@id` value of `Figure` in step [5](overriding-strings.md#change-strings), which overrides the default text found in **org.dita.base**.

    ```
    <xsl:call-template name="getVariable">
      <xsl:with-param name="id" select="Figure"/>
    </xsl:call-template>
    ```


**Related information**  


[How to add or modify generated text strings](../topics/plugin-addgeneratedtext.md)

