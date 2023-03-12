# Using the Java API

DITA Open Toolkit includes a Java Application Programming Interface to allow developers to embed the toolkit more easily into other Java programs.

When using the API, programmers don’t need to know or care that DITA-OT uses Ant, they can just use Java.

**Note:** When running DITA-OT via the dita command, an `ant` shell script handles the classpath setup, but when using the API the classpath should be set up as part of the normal classpath configuration for the Java application.

## Example usage

```
// Create a reusable processor factory with DITA-OT base directory
ProcessorFactory pf = ProcessorFactory.newInstance(ditaDir);
// and set the temporary directory
pf.setBaseTempDir(tempDir);

// Create a processor using the factory and configure the processor
Processor p = pf.newProcessor("html5")
.setInput(mapFile)
.setOutputDir(outDir)
.setProperty("nav-toc", "partial");

// Run conversion
p.run();
```

By default, running DITA-OT via the API will write a debug log to the temporary directory. A custom SLF4J logger can also be used to access the log via the Simple Logging Facade for Java.

The processor cleans the temporary directory by default, but this can be disabled to simplify debugging in cases where the processor failed.

**Tip:** See the **DITA-OT Java API documentation** in the doc/api/ folder of the DITA-OT distribution package for information on the packages, classes, interfaces and methods provided by the Java API.

## Downloading DITA-OT from Maven Central

As of version 2.5, the DITA Open Toolkit base library \(dost.jar\) is available via the Maven 2 Central Repository. You can use this mechanism to download the main JAR file and include it in the build for other Java projects.

To locate the latest version, [search for the `org.dita-ot` group ID](https://search.maven.org/#search%7Cga%7C1%7Cg%3A%22org.dita-ot%22).

**Important:** The dost.jar file provides only the DITA Open Toolkit base library. It does **not** contain the full DITA-OT distribution and cannot be used to run DITA-OT by itself. You will need to ensure that your build installs the other files and directories required for the toolkit along with the dependencies for your project.

**Related information**  


[DITA-OT Java API documentation](../api/index.html)

