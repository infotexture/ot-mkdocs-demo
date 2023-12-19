# Rebuilding the DITA-OT documentation

When you add or remove plug-ins, you can rebuild the documentation to update the information on the extension points, messages, and parameters that are available in your environment.

DITA-OT ships with a [Gradle](https://gradle.org) build script that enables you to rebuild the toolkit documentation. The build script reads the toolkit’s plug-in configuration and automatically regenerates topics and properties file templates based on the extension points, messages, and parameters provided by the installed plug-ins.

**Attention:** If you have installed new plug-ins, you may need to add the corresponding generated topics to the DITA maps to include the new information in the output.

1.  Change to the `docsrc/` subdirectory of the DITA-OT installation.

2.  Run one of the following commands.

    -   On Linux and macOS:

        ```
        ./gradlew *target*
        ```

    -   On Windows:

        ```
        gradlew.bat *target*
        ```

    The *target* parameter is optional and specifies a transformation type. It takes the following values:

    -   html
    -   htmlhelp
    -   pdf
    If you do not specify a target, HTML5 and PDF output is generated.


