# Arguments and options for the dita command

The dita command takes mandatory arguments to process DITA content. Subcommands can be used to manage plug-ins, or print information about the current configuration. A series of options are available to modify the command behavior or specify additional configuration parameters.

## Usage

To convert content from one format to another, specify the file to transform and the desired output format. If necessary, you can set additional configuration parameters with options.



> `**dita**` `**--input**` `=` *file* `**--format**` `=` *name* \[ *options* \]



> `**dita**` `**--project**` `=` *file* \[ *options* \]

**Note:** Most dita command options support several syntax alternatives. All options can be specified with a GNU-style option keyword preceded by two hyphens. In many cases, Unix-style single-letter options \(preceded by a single hyphen\) are also available for brevity and backwards compatibility.

The dita command also supports a series of subcommands that can be used to manage plug-ins, or print information about the current configuration or version.



> `**dita**` `**deliverables**` *file*



> `**dita**` `**install**` \[ \{ *ID* *\| URL* *\| file* \} \]



> `**dita**` `**plugins**`



> `**dita**` `**transtypes**`



> `**dita**` `**uninstall**` *ID*



> `**dita**` `**version**`

**Attention:** Prior to DITA-OT 3.5, subcommands were specified with the double-hyphen option syntax, which is still supported for backwards compatibility. \(For example, dita --install will still work.\)

## Arguments

Each transformation requires you to specify at least the file to transform and the desired output format.

-   **--input=file -i file**

    Specifies the master file for your documentation project. This argument corresponds to the common parameter args.input. Typically this is a DITA map, however it also can be a DITA topic if you want to transform a single DITA file. The path can be absolute, relative to args.input.dir, or relative to the current directory if args.input.dir is not defined.

-   **--format=name -f name**

    Specifies the output format \(transformation type\).

    This argument corresponds to the common parameter transtype.

    To list the formats that are currently available in your environment, use dita transtypes.

    You can create plug-ins to add new output formats; by default, the following values are available:

    -   dita
    -   eclipsehelp
    -   html5
    -   htmlhelp
    -   markdown, markdown\_gitbook, and markdown\_github
    -   pdf
    -   xhtml
    **Tip:** See [DITA-OT transformations \(output formats\)](../topics/output-formats.md) for sample command line syntax and more information on each transformation.


## Subcommands

-   **deliverables file**

    Show a list of the available deliverables in the specified project file.

-   **install \{ ID \| URL \| file \} --install=\{ ID \| URL \| file \}**

    Install a single plug-in IDfrom the registry at [dita-ot.org/plugins](https://www.dita-ot.org/plugins) \(or a local registry\), from a remote URL, or a local ZIP file.

-   **install --install**

    If no ID, URL, or file argument is provided, the installation process reloads the current set of plug-ins from the plugins directory \(or any custom locations defined via the pluginsdir property in the configuration.properties file in the config directory\). This approach can be used to add or remove multiple plug-ins at once, or any individual plug-ins you have already copied to \(or removed from\) the plug-in directories. Any plug-ins added or removed in the process will be listed by their plug-in ID.

-   **uninstall ID --uninstall=ID**

    Remove the plug-in with the specified ID.

    For a list of the currently installed plug-in IDs, use dita plugins.

    **Attention:** The uninstall subcommand also removes the corresponding plug-in directory from the plugins folder.

-   **plugins --plugins**

    Show a list of the currently installed plug-ins.

-   **transtypes --transtypes**

    Show a list of the available output formats \(transformation types\).

    The entries in this list may be passed as values to the --format argument.

-   **version --version**

    Print version information and exit.


## Options

-   **--debug -d**

    Debug logging prints considerably more additional information. The debug log includes all information from the verbose log, plus details on Java classes, additional Ant properties and overrides, preprocessing filters, parameters, and stages, and the complete build sequence. Debug logging requires additional resources and can slow down the build process, so it should only be enabled when further details are required to diagnose problems.

-   **--output=dir -o dir**

    Specifies the path of the output directory; the path can be absolute or relative to the current directory.

    This argument corresponds to the common parameter output.dir. By default, the output is written to the out subdirectory of the current directory.

-   **--filter=files**

    Specifies filter file\(s\) used to include, exclude, or flag content. Relative paths are resolved against the current directory and internally converted to absolute paths.

    **Note:**

    To specify multiple filter files, use the system path separator character to delimit individual file paths \(semicolon ‘`;`’ on Windows, and colon ‘`:`’ on macOS and Linux\) and wrap the value in quotes:

    `--filter="filter1.ditaval;filter2.ditaval;filter3.ditaval"`

    As of DITA-OT 3.6, the --filter option can also be passed multiple times:

    `--filter=filter1.ditaval --filter=filter2.ditaval --filter=filter3.ditaval`

    DITAVAL files are evaluated in the order specified, so conditions specified in the first file take precedence over matching conditions specified in later files, just as conditions at the start of a DITAVAL document take precedence over matching conditions later in the same document.

-   **--force**

    Force-install an existing plug-in.

    Passed as an additional option to the installation subcommand: dita install plug-in-zip --force

-   **--help -h**

    Print a list of available arguments, options, and subcommands.

-   **--logfile=file -l file**

    Write logging messages to a file.

-   **--parameter=value -Dparameter=value**

    Specify a value for a DITA-OT or Ant build parameter.

    The GNU-style --parameter=value form is only available for parameters that are configured in the plug-in configuration file; the Java-style -D form can also be used to specify additional non-configured parameters or set system properties.

    Parameters not implemented by the specified transformation type or referenced in a .properties file are ignored.

    **Tip:** If you are building in different environments where the location of the input files is not consistent, set args.input.dir with the dita command and reference its value with `${args.input.dir}` in your .properties file.

-   **--propertyfile=file**

    Use build parameters defined in the referenced .properties file.

    Build parameters specified on the command line override those set in the .properties file.

-   **--repeat=N**

    Repeat the transformation N number of times.

    This option can be used by plug-in developers to measure performance. To run a conversion five times, for example, use --repeat=5. The duration of each execution will appear in the console when the final transformation is complete.

    ```
    $ dita --input=docsrc/samples/sequence.ditamap --format=html5 --repeat=5
    1 11281ms
    2 4132ms
    3 3690ms
    4 4337ms
    5 3634ms
    ```

-   **--resource=file -r file**

    Convert partial documentation sets by processing input with additional resources.

    For example, to process a single topic file with a map that contains key definitions, use a command like this:

    ```syntax-bash
    dita --input=topic.dita --resource=keys.ditamap --format=html5
    ```

    To convert a chapter map to HTML5 and insert related links from relationship tables in a separate map, use:

    ```syntax-bash
    dita --input=chapter.ditamap --resource=reltables.ditamap --format=html5
    ```

-   **--temp=dir -t dir**

    Specifies the location of the temporary directory.

    This argument corresponds to the common parameter dita.temp.dir.

-   **--verbose -v**

    Verbose logging prints additional information to the console, including directory settings, effective values for Ant properties, input/output files, and informational messages to assist in troubleshooting.


**Related information**  


[Building output using the dita command](../topics/build-using-dita-command.md)

[DITA-OT parameters](../parameters/parameters_intro.md)

[Internal Ant properties](../parameters/internal-ant-properties.md)

[Setting build parameters with .properties files](../topics/using-dita-properties-file.md)

[Accessing help for the dita command](../topics/dita-command-help.md)

