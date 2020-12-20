# Implementing Saxon extension functions

Plug-ins can contribute Saxon extension functions for use in XSLT transformations run by DITA Open Toolkit.

Starting with Saxon 9.2, the mechanism for implementing extension functions has changed such that Saxon HE, in particular, can no longer use the older “reflexive” mechanism for finding Java extension functions using a magic URL. Instead, you implement extension functions and then register them directly on the Saxon Configuration object. DITA-OT provides a dynamic mechanism to perform this registration for plug-in-provided extension functions.

To implement extension functions, you must do the following:

1.  Add your plug-in’s JAR file in the DITA-OT class path as described in [Adding a Java library to the classpath](plugin-javalib.md).
2.  For each function, implement a class that extends `net.sf.saxon.lib.ExtensionFunctionDefinition`. This class provides the namespace name and function name for the function as well as details about its arguments and so on. See [Integrated extension functions](http://www.saxonica.com/html/documentation9.8/extensibility/integratedfunctions) in the Saxon documentation.
3.  Include a file named net.sf.saxon.lib.ExtensionFunctionDefinition in the directory META-INF/services in the compiled JAR that your plug-in provides. Each line of the file must be the name of a class that implements `net.sf.saxon.lib.ExtensionFunctionDefinition`:

    ```
    com.example.saxon.functions.Add
    com.example.saxon.functions.Substract
    ```

    You can create the file using `service` elements in an Ant `jar` task:

    ```language-xml
    <jar destfile="${basedir}/target/lib/example-saxon.jar">
      ⋮
      <service type="net.sf.saxon.lib.ExtensionFunctionDefinition">
        <provider classname="com.example.saxon.functions.Add"/>
        <provider classname="com.example.saxon.functions.Subtract"/>
      </service>
      ⋮
    </jar>
    ```

4.  In your XSLT transformations, declare the namespace the functions are bound to:

    ```language-xml
    <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
                    xmlns:xs="http://www.w3.org/2001/XMLSchema"
                    **xmlns:eg="http://example.com/saxon-extensions"**
                    version="2.0">
    ```


You should then be able to use the extension functions as you would any other function:

```language-xml
<xsl:variable name="test" select="**eg:add\(1, 2\)**"/>
```

