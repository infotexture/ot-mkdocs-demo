# PDF plug-in structure

In cases that require substantial customizations, it is often useful to organize the files in a folder structure that mimics the hierarchy of the default PDF plug-in.

**Note:** For simpler customizations, you may want to structure your plug-in differently, but the information in this topic may help you to locate the files you need to customize.

The original Idiom plug-in used its own extension mechanism to provide overrides to the PDF transformation. With this approach, a dedicated Customization folder within the plug-in was used as a customization layer to store files that override the default behavior.

While this method is no longer recommended, the same organization principles can be used in custom PDF plug-ins to facilitate comparisons with the default settings in the base PDF plug-in and make it easier to migrate customizations to new toolkit versions.

```
.
├── build.properties.orig
├── catalog.xml.orig
└── fo/
    ├── attrs/
    │   └── custom.xsl.orig
    └── xsl/
        └── custom.xsl.orig
```

To begin creating a new custom plug-in, you can copy the contents of the customization layer template in plugins/org.dita.pdf2/Customization to a new folder that will serve as your new custom plug-in folder, such as plugins/com.company.pdf.

To mimic the hierarchy of the default PDF plug-in, you may want to add a cfg/ subfolder and move the contents of the fo/ folder to cfg/fo/.

DITA-OT provides template files that you can start with throughout the Customization directory structure. These files end in the suffix `.orig` \(for example, catalog.xml.orig\). To enable these files, remove the `.orig` suffix from the copies in your new custom plug-in folder. \(For example, rename catalog.xml.orig to catalog.xml\).

You can then make modifications to the copy in your custom plug-in folder, and copy any other files from the default PDF plug-in that you need to override, such as the page layouts in layout-masters.xsl, or the font-mappings.xml file that tells your PDF renderer which fonts to use and where to find them.

**Important:** Wherever possible, avoid copying entire XSL files from the PDF2 plug-in to your custom plug-in. Instead, copy only the specific attribute sets and templates that you want to override. For details, see [Plug-in coding conventions](plugin-coding-conventions.md).

Things you can currently override include:

-   Custom XSL via xsl/custom.xsl and attrs/custom.xsl
-   Layout overrides via layout-masters.xsl
-   Font overrides via font-mappings.xml
-   Per-locale variable overrides via common/vars/\[language\].xml
-   I18N configuration via i18n/\[language\].xml
-   Index configuration via index/\[language\].xml

When customizing any of these areas, modify the relevant file\(s\) in your custom plug-in folder. Then, to enable the changes in the publishing process, you find the corresponding entry for each file you modified in the catalog.xml file.

It should look like this:

```language-xml
<!--uri name="cfg:fo/attrs/custom.xsl" uri="fo/attrs/custom.xsl"/-->
```

Remove the comment markers `!--` and `--` to enable the change:

```language-xml
<uri name="cfg:fo/attrs/custom.xsl" uri="fo/attrs/custom.xsl"/>
```

Your customization should now be enabled as part of the publishing process.

```
.
├── plugin.xml
├── ant-include.xml
└── cfg/
    ├── catalog.xml
    ├── common/
    │   ├── artwork/
    │   │   ├── logo.svg
    │   └── vars/
    │       ├── strings.xml
    │       ├── en.xml
    └── fo/
        ├── attrs/
        │   ├── custom.xsl
        ├── font-mappings.xml
        ├── layout-masters.xsl
        └── xsl/
            └── custom.xsl
```

When your custom plug-in is installed, the files in its subfolders will override the out-of-the-box settings from their counterparts in org.dita.pdf2/cfg/fo/attrs and org.dita.pdf2/xsl/fo.

The following topics describe the contents of the base PDF plug-in subfolders and provide additional information on customizing various aspects of the default PDF output.

