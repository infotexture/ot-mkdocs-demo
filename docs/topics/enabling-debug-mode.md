# Enabling debug mode

Debug logging prints considerably more additional information. The debug log includes all information from the verbose log, plus details on Java classes, additional Ant properties and overrides, preprocessing filters, parameters, and stages, and the complete build sequence. The debug log can help you determine the root cause of a problem.

1.  From the command prompt, add the following parameters:

    |Application|Parameters|
    |-----------|----------|
    |**dita command**|--debug, -debug, or -d|
    |**Ant**|`-v -Dargs.debug=yes`|

    You also can add a `property` element to an Ant target in your build file, for example:

    ```language-xml
    <property name="args.debug" value="yes"/>
    ```

    **Attention:** Debug logging requires additional resources and can slow down the build process, so it should only be enabled when further details are required to diagnose problems.


