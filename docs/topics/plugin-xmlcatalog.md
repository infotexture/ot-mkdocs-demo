# Extending an XML catalog file

You can update either the main DITA-OT XML catalog or the XML catalog that is used by the PDF plug-in. This enables DITA-OT to support new specializations and document-type shells.

You can use the **dita.specialization.catalog.relative** and **org.dita.pdf2.catalog.relative** extension points to update the DITA-OT catalog files.

**Remember:** The **dita.specialization.catalog** extension is deprecated. Use **dita.specialization.catalog.relative** instead.

1.  Using the OASIS catalog format, create an XML catalog file that contains only the new values that you want to add to a DITA-OT catalog file.

2.  Create a `plugin.xml` file that contains the following content:

    ```
    <plugin id="*plugin-id*">
      <feature extension="*extension-point*" file="*file*"/>
    </plugin>
    ```

    where:

    -   *plugin-id* is the plug-in identifier, for example, `com.example.catalog`.
    -   *extension-point* is either **dita.specialization.catalog.relative** or **org.dita.pdf2.catalog.relative**.
    -   *file* is the name of the new catalog file, for example, `catalog-dita.xml`.
3.  Save the new XML catalog file to your plug-in. Be sure that the local file references are relative to the location of the catalog and plug-in.

4.  Use the `dita install` subcommand to install the plug-in.

    **Note:** For more information, see [Installing plug-ins](plugins-installing.md).


The catalog entries inside of the new catalog file are added to the core DITA-OT catalog file.

## Example

This example assumes that `catalog-dita.xml` contains an OASIS catalog for any document-type shells inside this plug-in. The catalog entries in `catalog-dita.xml` are relative to the catalog itself; when the plug-in is installed, they are added to the core DITA-OT catalog \(with the correct path\).

```
<plugin id="com.example.catalog">
  <feature extension="dita.specialization.catalog.relative"
           file="catalog-dita.xml"/>
</plugin>
```

**Related information**  


[General extension points](../extension-points/plugin-extension-points-general.md)

[Installing plug-ins](../topics/plugins-installing.md)

