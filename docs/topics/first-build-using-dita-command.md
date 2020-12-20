# Building output using the dita command

You can generate output using the dita command-line tool. Build parameters can be specified on the command line or with .properties files.

The DITA-OT client is a command-line tool with no graphical user interface. To verify that your installation works correctly, you can build output using the sample files included in the distribution package.

1.  Open a terminal window by typing the following in the search bar:

        |**Linux or macOS **|Type Terminal.|
    |**Windows**|Type Command Prompt.|

2.  At the command-line prompt, enter the following command:

    ```syntax-bash
    dita --input=input-file --format=format 
    ```

    where:

    -   input-file is the DITA map or DITA file that you want to process.
    -   format is the output format \(transformation type\). This argument corresponds to the common parameter transtype. Use the same values as for the transtype build parameter, for example html5 or pdf.

    If processing is successful, nothing is printed in the terminal window. The built output is written to the specified output directory \(by default, in the out subdirectory of the current directory\).


Run from dita-ot-dir/docsrc/samples, the following command generates HTML5 output for the sequence.ditamap file:

```
dita --input=sequence.ditamap --format=html5
```

Most builds require you to specify more options than are described in this topic.

**Related information**  


[More information about building output with the dita command](../topics/build-using-dita-command.md)

