# Installing plug-ins

Use the `dita install` subcommand to install plug-ins.

1.  At the command-line prompt, enter the following command:

    ```syntax-bash
    `dita install` *&lt;plug-in&gt;*
    ```

    where:

    -   the optional `*&lt;plug-in&gt;*` argument is one of the following:
        -   the unique *ID* of the plug-in as defined in the plug-in registry at [dita-ot.org/plugins](https://www.dita-ot.org/plugins) \(or a local registry\)
        -   the remote *URL* of the plug-in’s distribution ZIP file
        -   the name of a local ZIP *file*
    **Note:** In earlier versions of DITA-OT \(2.4–3.4\), use the double-hyphen option syntax `dita` **--install**. In DITA-OT 2.0–2.3, use the single-hyphen form: `dita` **-install**.

    **Tip:** If no *ID*, *URL*, or *file* argument is provided, the installation process reloads the current set of plug-ins from the `plugins` directory \(or any custom locations defined via the **pluginsdir** property in the `configuration.properties` file in the `config` directory\). This approach can be used to add or remove multiple plug-ins at once, or any individual plug-ins you have already copied to \(or removed from\) the plug-in directories. Any plug-ins added or removed in the process will be listed by their plug-in ID.


**Related information**  


[Creating custom plug-ins](../topics/custom-plugins.md)

[Adding plug-ins via the registry](../topics/plugins-registry.md)

[The configuration.properties file](../parameters/configuration-properties-file.md)

[Arguments and options for the dita command](../parameters/dita-command-arguments.md)

[Plug-in installation made easier](https://www.oxygenxml.com/events/2018/dita-ot_day.html#plug-in_installation_made_easier)

