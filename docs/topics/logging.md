# Logging build information

When you run DITA-OT, key information is logged on the screen. This information can also be written to a log file. If you encounter a problem, you can analyze this information to determine the source of the problem and then take action to resolve it.

The logging behavior varies depending on whether you use the dita command or Ant to invoke a toolkit build.

-   **dita command**

    By default, only warning and error messages are written to the screen.

    -   For more information, enable verbose logging with dita --verbose.

        Verbose logging prints additional information to the console, including directory settings, effective values for Ant properties, input/output files, and informational messages to assist in troubleshooting.

    -   To enable debug logging, use dita --debug.

        Debug logging prints considerably more additional information. The debug log includes all information from the verbose log, plus details on Java classes, additional Ant properties and overrides, preprocessing filters, parameters, and stages, and the complete build sequence.

        **Attention:** Debug logging requires additional resources and can slow down the build process, so it should only be enabled when further details are required to diagnose problems.

    -   To write the log to a file, use dita --logfile=file and specify the path to the log file.

        Unless an absolute path is specified, the value will be interpreted relative to the current directory.

-   **Ant**

    By default, status information is written to the screen. If you issue the -l parameter, the build runs silently and the information is written to a log file with the name and location that you specified.


## Using other Ant loggers

You also can use other Ant loggers; see [Listeners & Loggers](https://ant.apache.org/manual/listeners.html) in the Ant documentation for more information.

For example, you can use the **AnsiColorLogger** to colorize the messages written on the screen.

-   **dita command**

    To use a custom Ant logger with the dita command, add the logger to the `ANT_ARGS` environment variable by calling the following command before calling the dita command:

    ```syntax-bash
    export ANT_ARGS="-logger org.apache.tools.ant.listener.AnsiColorLogger"
    ```

    Now you will get colorized messages when the dita command runs.

    **Tip:** Environment variables can also be set permanently. See [How do I set or change the PATH system variable?](https://www.java.com/en/download/help/path.xml) for information on how to set the [PATH environment variable](https://en.wikipedia.org/wiki/PATH_(variable)). You can set the `ANT_ARGS` environment variable in the same way.

-   **Ant**

    If you prefer to launch DITA-OT directly from Ant, you can also add the logger to the `ANT_ARGS` environment variable, as explained above. You can also set the logger with the `-logger` parameter when calling Ant.

    ```syntax-bash
    ant -logger org.apache.tools.ant.listener.AnsiColorLogger
    ```


## FOP debug logging

In PDF processing with Apache™ FOP, DITA-OT uses the Simple Logging Facade for Java \(SLF4J\) for better control and formatting of FOP log messages. To reduce noise on the console, all FOP messages are set to the Info level and hidden by default.

To enable debug logging, modify the config/logback.xml file or add your own logback.xml to the classpath with a higher priority to override the default settings. For more information, see the [Logback configuration documentation](https://logback.qos.ch/manual/configuration.html).

**Attention:** Enabling FOP debug logging will dramatically increase the size of generated log files.

