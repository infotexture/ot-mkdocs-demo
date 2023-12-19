# Speeding up builds

Several configuration changes can significantly reduce DITA-OT processing time.

## Disable debug attribute generation

The **generate-debug-attributes** parameter determines whether debugging attributes are generated in the temporary files. By changing the value to `false`, DITA-OT will no longer generate the `@xtrf` and `@xtrc` debug attributes. This will make it more difficult to track down the source file location from which a given issue may have originated, but it will reduce the size of the temporary files. As a result, XML parsing will take less time and overall processing time will be reduced.

## Use a fast disk for the temporary directory

DITA-OT keeps topic and map files as separate files and processes each file multiple times during preprocessing. Thus reading from disk, parsing XML, serializing XML, and writing to disk makes processing quite I/O intensive. Use either an [SSD](http://en.wikipedia.org/wiki/Solid-state_drive) or a [RAM disk](http://en.wikipedia.org/wiki/RAM_drive) for temporary files, and never use a temporary directory that is not located on the same machine as where the processing takes place.

## Enable parallel processing

As of DITA-OT 3.6, preprocessing module code can be run in parallel by setting the **parallel** parameter to true. The performance benefits this option provides depend heavily on the source file set, the DITA features used in the project, and the computer doing the processing, but under the right circumstances, you may see notable improvements when this option is enabled.

## Enable in-memory processing

As of DITA-OT 3.6, the Cache Store can be activated by setting the **store-type** parameter to memory. In-memory processing provides performance advantages in I/O bound environments such as cloud computing platforms, where processing time depends primarily on how long it takes to read and write temporary files. For more information, see [Store API – Processing in memory](../reference/store-api.md).

## Reuse the JVM instance

For all but large source sets, the Java virtual machine \(JVM\) will not have enough time to warm-up. By reusing the same JVM instance, the first few DITA-OT conversions will be “normal”, but when the Just-In-Time \(JIT\) compiler starts to kick in, the performance increase may be 2-10 fold. This is especially noticeable with smaller source sets, as much of the DITA-OT processing is I/O intensive.

**Tip:** The [Gradle Daemon](https://docs.gradle.org/current/userguide/gradle_daemon.html) uses this mechanism \(along with incremental builds\) to reduce processing time. You can run DITA-OT with these features via the [DITA-OT Gradle Plugin](https://github.com/eerohele/dita-ot-gradle).

## Use the latest Java version

DITA-OT 2.0 to 2.3 require Java 7, and DITA-OT 2.4 and newer require Java 8. However, using a newer version of Java may further reduce processing time, depending on your operating system.

## Re-enable Java file caching

As of Java 12, the file canonicalization cache is no longer enabled by default \(see [JDK-8207005](https://bugs.openjdk.org/browse/JDK-8207005)\). On Windows, this results in significantly longer build times, and slight increases on Linux. To re-enable file caching, add `-Dsun.io.useCanonCaches=true` to the Java invocation command in the `dita.bat` and `ant.bat` wrapper scripts.

**Note:** As of DITA-OT 3.7.3, this system property is set by default in the bundled wrapper scripts.

**Collected links**  


[SSD](http://en.wikipedia.org/wiki/Solid-state_drive)

[RAM disk](http://en.wikipedia.org/wiki/RAM_drive)

