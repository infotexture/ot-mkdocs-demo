# Building output using the `dita` command

You can generate output using the `dita` command-line tool. Build parameters can be specified on the command line or with `.properties` files.

1.  At the command-line prompt, enter the following command:

    ```syntax-bash
    ``dita`` **--input**=*input-file* **--format**=*format* \[*options*\]
    ```

    where:

    -   *input-file* is the DITA map or DITA file that you want to process.
    -   *format* is the output format \(transformation type\). This argument corresponds to the common parameter [transtype](../parameters/parameters-base.md#transtype). Use the same values as for the **transtype** build parameter, for example html5 or pdf.

        You can create plug-ins to add new output formats; by default, the following values are available:

        -   dita
        -   eclipsehelp
        -   html5
        -   htmlhelp
        -   markdown, markdown\_gitbook, and markdown\_github
        -   pdf
        -   xhtml
        **Tip:** See [DITA-OT transformations \(output formats\)](output-formats.md) for sample command line syntax and more information on each transformation.

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


For example, from `*dita-ot-dir*/docsrc/samples`, run:

```
`dita` **--input**=`sequence.ditamap` **--format**=html5 \
     **--output**=`output/sequence` \
     **--args.input.dir**=`*/absolute/path/to/dita-ot-dir*/docsrc/samples` \
     **--propertyfile**=`properties/sequence-html5.properties`
```

This builds `sequence.ditamap` to HTML5 output in `output/sequence` using the following additional parameters specified in the `properties/sequence-html5.properties` file:

```
# Directory that contains the custom .css file:
args.cssroot = ${args.input.dir}/css/

# Custom .css file used to style output:
args.css = style.css

# Copy the custom .css file to the output directory:
args.copycss = yes

# Location of the copied .css file relative to the output:
args.csspath = branding

# Generate a full navigation TOC in topic pages:
nav-toc = full
```

Usually, you will want to specify a set of reusable build parameters in a `.properties` file.

**Related information**  


[Arguments and options for the dita command](../parameters/dita-command-arguments.md)

[Accessing help for the dita command](../topics/dita-command-help.md)

[DITA-OT parameters](../parameters/parameters_intro.md)

[Internal Ant properties](../parameters/internal-ant-properties.md)

[Why "startcmd" is not your friend](https://www.oxygenxml.com/events/2015/dita-ot_day.html#Why_startcmd_is_not_your_friend)

