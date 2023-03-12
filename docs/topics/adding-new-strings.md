# Adding new strings

Add new generated strings to your plug-in for the toolkit to include in your output.

1.  Copy this file to your plug-in.

    -   non-PDF output: plugins/org.dita.base/xsl/common/strings.xml
    -   PDF output: plugins/org.dita.pdf2/cfg/common/vars/strings.xml
2.  In your plug-in, edit strings.xml to contain references to the language files for which you are providing custom strings.

    The `en-US` language must be present; other language files are optional.

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <!-- Provide strings for my plug-in; this plug-in supports
         English, Icelandic, and Russian. -->
    <langlist>
      <lang xml:lang="en"     filename="my-added-strings-en-us.xml"/>
      <lang xml:lang="en-US"  filename="my-added-strings-en-us.xml"/>
      <lang xml:lang="is"     filename="my-added-strings-is-is.xml"/>
      <lang xml:lang="is-IS"  filename="my-added-strings-is-is.xml"/>
      <lang xml:lang="ru"     filename="my-added-strings-ru-ru.xml"/>
      <lang xml:lang="ru-RU"  filename="my-added-strings-ru-ru.xml"/>
    </langlist>
    ```

3.  In xsl/common or cfg/common/vars, create a new file called my-added-strings-en-us.xml.

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <variables>
    
    </variables>
    ```

4.  For each new string you want, add a `variable` element with an `@id` attribute and the text you want the toolkit to use.

    The `@id` attribute value must be unique in the file and should reflect the purpose of the generated text.

    The toolkit uses the text found inside the element when inserting generated text.

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <variables>
      <variable id="String1">English generated text</variable>
      <variable id="Another String">Another string in English</variable>
    </variables>
    ```

5.  Repeat step [3](adding-new-strings.md#copy-strings) and step [4](adding-new-strings.md#create-strings) for each language.

6.  Update your plugin.xml file to extend the strings available.

    ```
    <plugin id="com.example.your-plugin">
      <feature extension="dita.xsl.strings" file="xsl/common/strings.xml"/>
    </plugin>
    ```

    Your custom strings are available to your stylesheets. For example, if processing in a context where the `@xml:lang` value is `en-US`, the following call returns **“Another string in English”** because it was defined as the text for the variable with `@id` value of `Another String` in step [4](adding-new-strings.md#create-strings).

    ```
    <xsl:call-template name="getVariable">
      <xsl:with-param name="id" select="'Another String'"/>
    </xsl:call-template>
    ```

    You can also use the same strings in multiple languages by assigning a file with common strings to each language in addition to the language-specific custom strings files.

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <langlist>
      <lang xml:lang="en"     filename="my-added-strings-en-us.xml"/>
      <lang xml:lang="en-US"  filename="my-added-strings-en-us.xml"/>
      **&lt;lang xml:lang="en"     filename="my-added-strings-mul.xml"/&gt;**
      **&lt;lang xml:lang="en-US"  filename="my-added-strings-mul.xml"/&gt;**
      <lang xml:lang="is"     filename="my-added-strings-is-is.xml"/>
      <lang xml:lang="is-IS"  filename="my-added-strings-is-is.xml"/>
      **&lt;lang xml:lang="is"     filename="my-added-strings-mul.xml"/&gt;**
      **&lt;lang xml:lang="is-IS"  filename="my-added-strings-mul.xml"/&gt;**
      <lang xml:lang="ru"     filename="my-added-strings-ru-ru.xml"/>
      <lang xml:lang="ru-RU"  filename="my-added-strings-ru-ru.xml"/>
      **&lt;lang xml:lang="ru"     filename="my-added-strings-mul.xml"/&gt;**
      **&lt;lang xml:lang="ru-RU"  filename="my-added-strings-mul.xml"/&gt;**
    </langlist>
    ```


**Related information**  


[How to add or modify generated text strings](../topics/plugin-addgeneratedtext.md)

