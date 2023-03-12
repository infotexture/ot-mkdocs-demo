# Prerequisite software

The software that DITA-OT requires depends on the output formats you want to use.

## Software required for core DITA-OT processing

DITA-OT requires the following software applications:

-   **Java Runtime Environment \(JRE\) or Java Development Kit \(JDK\)**

    DITA-OT 4.0 is designed to run on Java version 17 or later and built and tested with the Open Java Development Kit \(OpenJDK\). Compatible Java distributions are available from multiple sources:

    -   You can download the Oracle JRE or JDK from [oracle.com/java](https://www.oracle.com/java/technologies/downloads/) under commercial license.
    -   Eclipse Temurin is the free OpenJDK distribution available from [adoptium.net](https://adoptium.net/temurin/releases/?version=17).
    -   Free OpenJDK distributions are also provided by [Amazon Corretto](https://aws.amazon.com/corretto/), [Azul Zulu](https://www.azul.com/downloads/), and [Red Hat](https://developers.redhat.com/products/openjdk/download).
    **Note:** This is the *only* prerequisite that you need to install. All other required software is provided in the distribution package, including [Apache Ant™](https://ant.apache.org) 1.10.12, [Saxon](http://saxon.sourceforge.net) 10.6, and [ICU for Java](http://site.icu-project.org/download) 70.1.


## Software required for specific transformations

Depending on the type of output that you want to generate, you might need the following applications:

-   **Microsoft Help Workshop**

    Required for generating HTML help. You can download the Help Workshop from [msdn.microsoft.com](http://msdn.microsoft.com/en-us/library/windows/desktop/ms669985%28v=vs.85%29.aspx).

-   **XSL-FO processor**

    Required for generating PDF output. Apache™ FOP **\(Formatting Objects Processor\)** 2.5 is included in the distribution package. You can download other versions from [xmlgraphics.apache.org/fop](https://xmlgraphics.apache.org/fop/download.html). You can also use commercial FO processors such as Antenna House Formatter or RenderX XEP.


