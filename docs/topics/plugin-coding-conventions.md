# Plug-in coding conventions

To ensure custom plug-ins work well with the core toolkit code and remain compatible with future releases, the DITA Open Toolkit project recommends that plug-ins use modern development practices and common coding patterns.

## Best practices

Adhering to certain development practices will properly isolate your code from that of DITA Open Toolkit. This will make it easier to you to upgrade to new versions of DITA-OT when they are released.

-   Use a properly-constructed DITA-OT plug-in.

-   Use a version control system to store your code.

-   Store the source code of your plug-ins outside of the DITA-OT installation directory, and add the repository location to the list of plug-in directories defined in the plugindirs entry of the [configuration.properties file](../parameters/configuration-properties-file.md).

-   Never modify any of the core DITA-OT code.

    **Tip:** You may want to set the permissions on default plug-in directories such as org.dita.pdf2 to “read-only” to ensure that you do not accidentally modify the files within as you develop your customized plug-in.

-   Avoid copying entire DITA-OT files into your customization plug-in. When you only copy the attribute sets and templates that you need to override, there is less risk of impact from new features or fixes in the base code, making your code more stable and easier to upgrade between releases.

-   If you only need to change a few attribute sets and templates, you may prefer to store your overrides in custom.xsl files, or a simple folder hierarchy within your custom plug-in.

-   In cases that require substantial customizations, you may prefer to organize the files in a folder structure that mimics the hierarchy of the default plug-in you are customizing. This facilitates comparisons with the default settings in the base plug-in and makes it easier to migrate your changes to new toolkit versions. See [PDF plug-in structure](pdf-plugin-structure.md) for information on the files in the base PDF plug-in.

-   Upgrade your customization plug-in to new versions of DITA-OT regularly. Do not wait through several major releases before upgrading.


## Use a custom namespace

For XSLT customizations, use a custom namespace for any modified template modes, template names, attribute sets, functions, and variables. This helps to clarify which portions of the code are specific to your customizations, and serves to isolate your changes in the event that items with the same name are added to the base plug-ins in the future.

For example, instead of creating a template named `searchbar`, use something like `corp:searchbar` instead. This ensures that if future versions of DITA-OT add a `searchbar` template, your custom version will be unaffected.

Instead of:

```language-xml
<xsl:template name="searchbar"/>
```

use:

```language-xml
<xsl:template name="corp:searchbar"/>
```

## Upgrade stylesheets to XSLT 2.0

The Saxon project has announced plans to remove XSLT 1.0 support from the Saxon-HE library that ships with DITA-OT:

> …we’re dropping XSLT 1.0 backwards compatibility mode from Saxon-HE, and hope to eliminate it entirely in due course.

> [*https://www.xml.com/news/release-saxon-98/*](https://www.xml.com/news/release-saxon-98/)

DITA-OT 3.0 and 3.0.1 included Saxon-HE 9.8.0.5, which rejects XSLT stylesheets that specify `version="1.0"`. Plug-ins with XSLT templates specifying version 1.0 will fail with the message “XSLT 1.0 compatibility mode is not available in this configuration.”

To resolve this issue, change any occurrences of `<xsl:stylesheet version="1.0">` in custom plug-in stylesheets to at least `<xsl:stylesheet version="2.0">`.

**Tip:** DITA-OT 3.0.2 includes Saxon-HE 9.8.0.7, which restores XSLT 1.0 backwards-compatibility mode, but the DITA Open Toolkit project recommends upgrading all stylesheets to XSLT 2.0 to ensure plug-ins remain compatible with future versions of DITA-OT and Saxon-HE.

## Use custom `pipeline` elements

In Ant scripts, use the XSLT module from DITA-OT instead of Ant’s built-in `xslt` or `style` tasks.

The XSLT module allows access to DITA-OT features like using the job configuration to select files in the temporary folder based on file metadata and custom XSLT extension functions.

**Important:** Future versions of DITA-OT may switch to a new XML resolver or in-memory storage features that are not supported by Ant’s XSLT task. To ensure compatibility with future releases, plug-ins should replace these constructs with custom `pipeline` elements.

Instead of:

```
<xslt style="${dita.plugin.example.dir}/custom.xsl"
      basedir="${dita.temp.dir}"
      destdir="${dita.output.dir}"
      includesfile="${dita.temp.dir}/${fullditatopicfile}"/>
```

use:

```
<pipeline>
  <xslt style="${dita.plugin.example.dir}/custom.xsl"
        destdir="${dita.output.dir}">
    <ditafileset format="dita" />
  </xslt>
</pipeline>
```

## Use the plug-in directory property

In Ant scripts, always refer to files in other plug-ins using the `dita.plugin.plugin-id.dir` property.

Instead of:

```language-xml
<property name="base" location="../example/custom.xsl"/>
```

use:

```language-xml
<property name="base" location="${dita.plugin.example.dir}/custom.xsl"/>
```

This fixes cases where plug-ins are installed to custom plug-in directories or the plug-in folder name doesn’t match the plug-in ID.

**Tip:** For details, see [Referencing files from other plug-ins](referencing-other-plugins.md).

## Use the `plugin` URI scheme

In XSLT, use the `plugin` URI scheme in `xsl:import` and `xsl:include` to reference files in other plug-ins.

Instead of:

```language-xml
<xsl:import href="../../org.dita.base/xsl/common/output-message.xsl"/>
```

use:

```language-xml
<xsl:import href="plugin:org.dita.base:xsl/common/output-message.xsl"/>
```

As with the plug-in directory property in Ant, this allows plug-ins to resolve to the correct directory even when a plug-in moves to a new location. The plug-in is referenced using the syntax `plugin:plugin-id:path/within/plugin/file.xsl`.

**Tip:** For details, see [Referencing files from other plug-ins](referencing-other-plugins.md).

## Use `ditafileset` to select files

In Ant scripts, use `ditafileset` to select resources in the temporary directory.

For example, to select all images referenced by input DITA files, instead of:

```
<copy todir="${copy-image.todir}">
  <fileset dir="${user.input.dir}">
    <includes name="*.jpg"/>
    <includes name="*.jpeg"/>
    <includes name="*.png"/>
    <includes name="*.gif"/>
    <includes name="*.svg"/>
  </fileset>
</copy>
```

use:

```
<copy todir="${copy-image.todir}">
  <ditafileset format="image" />
</copy>
```

The `ditafileset` resource collection can be used to select different types of files.

|Example|Description|
|-------|-----------|
|`<ditafileset format="dita"/>`|Selects all DITA topics in the temporary directory.|
|`<ditafileset format="ditamap"/>`|Selects all DITA maps in the temporary directory.|
|`<ditafileset format="image"/>`|Selects images of all known types in the temporary directory.|

## Validating plug-ins

DITA-OT includes a RELAX NG schema file that can be used to validate the plugin.xml files that define the capabilities of each plug-in.

To ensure the syntax of your custom plug-in is correct, include an `xml-model` processing instruction at the beginning of the plugin.xml file, immediately after the XML prolog:

`xml-model href="dita-ot/plugin.rnc" type="application/relax-ng-compact-syntax"`

If your authoring environment does not apply this schema automatically, point your editor to dita-ot-dir/resources/plugin.rnc to associate the schema with your plug-in file.

**Related information**  


[Custom HTML plug-ins](../topics/html-customization-plugins.md)

[Custom PDF plug-ins](../topics/pdf-customization-plugins.md)

[Plug-in dependencies](../topics/plugin-dependencies.md)

[Referencing files from other plug-ins](../topics/referencing-other-plugins.md)

[Validation meets publication - Apply your style guide rules during the publication](https://www.oxygenxml.com/events/2018/dita-ot_day.html#apply_your_style_guide_rules_during_the_publication)

[Unit Testing DITA-OT Plugin Extensions](https://www.oxygenxml.com/events/2018/dita-ot_day.html#unit_testing_DITA-OT_plugin_extensions)

[Meta DITA samples: testing around the edge cases](https://www.oxygenxml.com/events/2018/dita-ot_day.html#meta_DITA_samples)

[Managing a large scale build environment with 50+ custom plugins](https://www.oxygenxml.com/events/2017/dita-ot_day.html#Managing_a_large_scale_build_environment)

[DITA-OT Patterns and Anti-patterns](https://www.oxygenxml.com/events/2015/dita-ot_day.html#DITA-OT_Patterns_and_Anti-patterns)

[Multiple OT with Git](https://www.oxygenxml.com/events/2015/dita-ot_day.html#Multiple_OT_With_Git)

