# Removing plug-ins

Use the dita uninstall subcommand to remove a plug-in.

1.  At the command-line prompt, enter the following command:

    ```syntax-bash
    dita uninstall &lt;plug-in-id&gt;
    ```

    where:

    -   &lt;plug-in-id&gt; is the unique ID of the plug-in, as defined in the plug-in’s configuration file \(plugin.xml\).
    **Note:** In earlier versions of DITA-OT \(2.4–3.4\), use the double-hyphen option syntax dita --uninstall. In DITA-OT 2.0–2.3, use the single-hyphen form: dita -uninstall.

    **Attention:** The uninstall subcommand also removes the corresponding plug-in directory from the plugins folder.


**Related information**  


[Arguments and options for the dita command](../parameters/dita-command-arguments.md)

[Trim your toolkit with this one weird trick!](https://www.oxygenxml.com/events/2019/dita-ot_day.html#trim_your_toolkit)

