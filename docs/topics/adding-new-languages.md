# Adding new languages

Extend the toolkit’s generated text capabilities by adding new language files.

1.  Copy this file to your plug-in.

    -   non-PDF output: plugins/org.dita.base/xsl/common/strings.xml
    -   PDF output: plugins/org.dita.pdf2/cfg/common/vars/strings.xml
2.  In your plug-in, edit strings.xml to contain references to the language files for which you are providing custom strings.

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <!-- Provide new languages for Gaelic and Vietnamese. -->
    <langlist>
      <lang xml:lang="ga"     filename="strings-ga-ga.xml"/>
      <lang xml:lang="ga-GA"  filename="strings-ga-ga.xml"/>
      <lang xml:lang="vi"     filename="strings-vi-vn.xml"/>
      <lang xml:lang="vi-VN"  filename="strings-vi-vn.xml"/>
    </langlist>
    ```

3.  Copy this file to your plug-in into the same directory as step [1](adding-new-languages.md#copy-strings-xml).

    -   non-PDF output: plugins/org.dita.base/xsl/common/strings-en-us.xml
    -   PDF output: plugins/org.dita.pdf2/cfg/common/vars/en.xml
4.  Rename the file to match the language you wish to add \(for instance, strings-vi-vn.xml\).

5.  Without changing the `@id` value, replace the generated text string for each variable.

    ```
    <variables>
       <variable id="Figure">Hình</variable>
       <variable id="Table">Bảng</variable>
       <variable id="Next topic">Chủ đề tiếp theo</variable>
         [...]
       <variable id="Copyright">Bản quyền</variable>
       <variable id="a11y.and-then"/>
    </variables>
    ```

6.  Repeat step [3](adding-new-languages.md#copy-strings) to step [5](adding-new-languages.md#replace-strings) for each language.

7.  Update your plugin.xml file to extend the strings available.

    ```
    <plugin id="com.example.your-plugin">
      <feature extension="dita.xsl.strings" file="xsl/common/strings.xml"/>
    </plugin>
    ```

    Your custom language strings are available to your stylesheets. For example, if processing in a context where the `@xml:lang` value is `vi-VN`, the following call returns **“Chủ đề tiếp theo”** because it was defined as the text for the variable with `@id` value of `Next topic` in step [5](adding-new-languages.md#replace-strings).

    ```
    <xsl:call-template name="getVariable">
      <xsl:with-param name="id" select="'Next topic'"/>
    </xsl:call-template>
    ```


**Related information**  


[How to add or modify generated text strings](../topics/plugin-addgeneratedtext.md)

