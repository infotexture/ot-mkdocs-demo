# Conref file for tasks

DITA-OT releases follow [semantic versioning](https://semver.org) guidelines. Version numbers use the *major.minor.patch* syntax, where *major* versions may include incompatible API changes, *minor* versions add functionality in a backwards-compatible manner and *patch* versions are maintenance releases that include backwards-compatible bug fixes.

Custom plug-ins developed for a previous *major* version may require changes to work correctly with recent toolkit versions. Most plug-ins should be compatible with subsequent *minor* and *patch* versions of the *major* release for which they were originally developed.

-   **Standard Path / Directory Names**

    `*dita-ot-dir*`

    ``dita``

    `*dita-ot-dir*/docsrc`

    `*dita-ot-dir*/docsrc/samples`

    `*/absolute/path/to/dita-ot-dir*/docsrc/samples`

-   **Plug-In Info**
    -   `*&lt;plug-in-id&gt;*` is the unique ID of the plug-in, as defined in the plug-in’s configuration file \(`plugin.xml`\).
    -   `*plug-in-zip*` is the *filename* or *URL* of the plug-in’s distribution ZIP file \(optional\).
    -   the optional `*&lt;plug-in&gt;*` argument is one of the following:
        -   the unique *ID* of the plug-in as defined in the plug-in registry at [dita-ot.org/plugins](https://www.dita-ot.org/plugins) \(or a local registry\)
        -   the remote *URL* of the plug-in’s distribution ZIP file
        -   the name of a local ZIP *file*
    -   If no *ID*, *URL*, or *file* argument is provided, the installation process reloads the current set of plug-ins from the `plugins` directory \(or any custom locations defined via the **pluginsdir** property in the `configuration.properties` file in the `config` directory\). This approach can be used to add or remove multiple plug-ins at once, or any individual plug-ins you have already copied to \(or removed from\) the plug-in directories. Any plug-ins added or removed in the process will be listed by their plug-in ID.
    -   **Attention:** The `uninstall` subcommand also removes the corresponding plug-in directory from the `plugins` folder.

    -   **Note:** In earlier versions of DITA-OT \(2.4–3.4\), use the double-hyphen option syntax `dita` **--uninstall**. In DITA-OT 2.0–2.3, use the single-hyphen form: `dita`


1.  Download the `dita-ot-4.1.2.zip` package from the project website at [dita-ot.org/download](https://www.dita-ot.org/download).

2.  Open a command prompt or terminal session.

    -   *input-file* is the DITA map or DITA file that you want to process.
    -   *format* is the output format \(transformation type\). This argument corresponds to the common parameter [transtype](../parameters/parameters-base.md#transtype). Use the same values as for the **transtype** build parameter, for example html5 or pdf.

    -   *format* is the output format \(transformation type\). This argument corresponds to the common parameter [transtype](../parameters/parameters-base.md#transtype). Use the same values as for the **transtype** build parameter, for example html5 or pdf.

        You can create plug-ins to add new output formats; by default, the following values are available:

        -   dita
        -   eclipsehelp
        -   html5
        -   htmlhelp
        -   markdown, markdown\_gitbook, and markdown\_github
        -   pdf
        -   xhtml
        **Tip:** See [DITA-OT transformations \(output formats\)](../topics/output-formats.md) for sample command line syntax and more information on each transformation.

    -   \[*options*\] include the following optional build parameters:
        -   **__--debug__ __-d__**

            Debug logging prints considerably more additional information. The debug log includes all information from the verbose log, plus details on Java classes, additional Ant properties and overrides, preprocessing filters, parameters, and stages, and the complete build sequence. Debug logging requires additional resources and can slow down the build process, so it should only be enabled when further details are required to diagnose problems.

        -   **__--output__=_dir_ __-o__ _dir_**

            Specifies the path of the output directory; the path can be absolute or relative to the current directory.

            This option corresponds to the common parameter [output.dir](../parameters/parameters-base.md#output.dir).

            By default, the output is written to the `out` subdirectory of the current directory.

        -   **__--filter__=_files_**

            Specifies filter file\(s\) used to include, exclude, or flag content. Relative paths are resolved against the current directory and internally converted to absolute paths.

            **Note:**

            To specify multiple filter files, use the system path separator character to delimit individual file paths \(semicolon ‘`;`’ on Windows, and colon ‘`:`’ on macOS and Linux\) and wrap the value in quotes:

            `--filter="filter1.ditaval;filter2.ditaval;filter3.ditaval"`

            As of DITA-OT 3.6, the **--filter** option can also be passed multiple times:

            `--filter=filter1.ditaval --filter=filter2.ditaval --filter=filter3.ditaval`

            DITAVAL files are evaluated in the order specified, so conditions specified in the first file take precedence over matching conditions specified in later files, just as conditions at the start of a DITAVAL document take precedence over matching conditions later in the same document.

        -   **__--force__**

            Force-install an existing plug-in.

            Passed as an additional option to the installation subcommand: `dita install` *plug-in-zip* **--force**

        -   **__--help__ __-h__**

            Print a list of available arguments, options, and subcommands.

        -   **__--logfile__=_file_ __-l__ _file_**

            Write logging messages to a file.

        -   **__--parameter__=_value_ __-D___parameter_=_value_**

            Specify a value for a DITA-OT or Ant build parameter.

            The GNU-style **--parameter**=*value* form is only available for parameters that are configured in the plug-in configuration file; the Java-style **-D** form can also be used to specify additional non-configured parameters or set system properties.

            Parameters not implemented by the specified transformation type or referenced in a `.properties` file are ignored.

            **Tip:** If you are building in different environments where the location of the input files is not consistent, set args.input.dir with the `dita` command and reference its value with `${args.input.dir}` in your `.properties` file.

        -   **__--propertyfile__=_file_**

            Use build parameters defined in the referenced `.properties` file.

            Build parameters specified on the command line override those set in the `.properties` file.

        -   **__--repeat__=_N_**

            Repeat the transformation *N* number of times.

            This option can be used by plug-in developers to measure performance. To run a conversion five times, for example, use **--repeat**=5. The duration of each execution will appear in the console when the final transformation is complete.

            ```
            $ `dita` **--input**=`docsrc/samples/sequence.ditamap` **--format**=html5 \
                   **--repeat**=5
            1 11281ms
            2 4132ms
            3 3690ms
            4 4337ms
            5 3634ms
            ```

        -   **__--resource__=_file_ __-r__ _file_**

            Specifies resource files.

            This argument corresponds to the common parameter [args.resources](../parameters/parameters-base.md#args.resources).

            Resource files can be used to convert partial documentation sets by processing input with additional information.

            For example, to process a single topic file with a map that contains key definitions, use a command like this:

            ```syntax-bash
            `dita` **--input**=`topic.dita` **--resource**=`keys.ditamap` **--format**=html5
            ```

            To convert a chapter map to HTML5 and insert related links from relationship tables in a separate map, use:

            ```syntax-bash
            `dita` **--input**=`chapter.ditamap` **--resource**=`reltables.ditamap` **--format**=html5
            ```

        -   **__--temp__=_dir_ __-t__ _dir_**

            Specifies the location of the temporary directory.

            This option corresponds to the common parameter [dita.temp.dir](../parameters/parameters-base.md#dita.temp.dir).

            The temporary directory is where DITA-OT writes intermediate files that are generated during the transformation process.

        -   **__--verbose__ __-v__**

            Verbose logging prints additional information to the console, including directory settings, effective values for Ant properties, input/output files, and informational messages to assist in troubleshooting.

    If processing is successful, nothing is printed in the terminal window. The built output is written to the specified output directory \(by default, in the `out` subdirectory of the current directory\).

3.  Extending pre-processing

    **Tip:** For maximum compatibility with future versions of DITA-OT, most plug-ins should use the extension points that run **before** or **after** pre-processing.

    CAUTION:

    The internal order of preprocessing steps is subject to change between versions of DITA-OT. New versions may remove, reorder, combine, or add steps to the process, so the extension points **within** the preprocessing stage should only be used if absolutely necessary.

4.  Use the `dita install` subcommand to install the plug-in.

    **Note:** For more information, see [Installing plug-ins](../topics/plugins-installing.md).


**Tip:** Copy `*dita-ot-dir*/docsrc/samples``/properties/template.properties`; this template describes each of the properties you can set.

**Tip:** If you are building in different environments where the location of the input files is not consistent, set args.input.dir with the `dita` command and reference its value with `${args.input.dir}` in your `.properties` file.

1.  Use the `dita install` subcommand to install the plug-in.

    **Note:** For more information, see [Installing plug-ins](../topics/plugins-installing.md).


