# Other error messages

In addition to error messages that DITA Open Toolkit generates, you might also encounter error messages generated by Java or other tools.

## Out of Memory error

In some cases, you might receive a message stating the build has failed due to an `Out of Memory` error. Try the following approaches to resolve the problem:

1.  Increase the memory available to Java.
2.  Reduce memory consumption by setting the generate-debug-attributes option to `false`. This option is set in the `lib/configuration.properties` file. This will disable debug attribute generation \(used to trace DITA-OT error messages back to source files\) and will reduce memory consumption.
3.  Set `dita.preprocess.reloadstylesheet` Ant property to `true`. This will allow the XSLT processor to release memory when converting multiple files.
4.  Run the transformation again.

## UnsupportedClassVersionError

If you receive a `java.lang.UnsupportedClassVersionError` error message with an `Unsupported major.minor version` and a list of Java classes, make sure your system meets the minimum Java requirements as listed in the **Release Notes** and installation instructions.

## Unable to locate tools.jar

If a Java Runtime Environment \(JRE\) is used when building output via Ant, the `Unable to locate tools.jar` error may appear. This message is safe to ignore, since DITA-OT does not rely on any of the functions in this library. If a Java Development Kit \(JDK\) is also installed, setting the *JAVA\_HOME* environment variable to the location of the JDK will prevent this message from appearing.

**Related information**  


[Increasing Java memory allocation](../topics/increasing-the-jvm.md)

[Other parameters](../parameters/parameters-other.md)

[DITA Open Toolkit 4.1 Release Notes](../release-notes/index.md)

[Installing DITA Open Toolkit](../topics/installing-client.md)

