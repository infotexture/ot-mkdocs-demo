# Prerequisite software

The prerequisite software that DITA-OT requires depends on the types of transformations that you want to use.

## Software required for core DITA-OT processing

DITA-OT requires the following software applications:

-   **Java Runtime Environment \(JRE\) or Java Development Kit \(JDK\)**

    DITA-OT is designed to run on Java version 8u101 or later and built and tested with the Open Java Development Kit \(OpenJDK\). Compatible Java distributions are available from multiple sources:

    -   You can download the Oracle JRE or JDK from [oracle.com/technetwork/java](http://www.oracle.com/technetwork/java/javase/downloads) under commercial license.
    -   OpenJDK is a free open-source implementation of Java available from [adoptopenjdk.net](https://adoptopenjdk.net).
    -   Free OpenJDK distributions are also available from other vendors, including [Amazon Corretto](https://aws.amazon.com/corretto/), [Azul Zulu](https://www.azul.com/downloads/zulu/), and [Red Hat](https://developers.redhat.com/products/openjdk/download).
    **Note:** This is the *only* prerequisite software that you need to install. The remaining required software is included in the distribution package.

-   **Apache Ant**

    Provides the standard setup and sequencing of processing steps. DITA-OT includes Ant version 1.10.9. You can download Ant from [ant.apache.org](https://ant.apache.org).

-   **XSLT processor**

    Provides the main transformation services. It must be compliant with XSLT 2.0. DITA-OT includes Saxon version 9.9.1.4. You can download Saxon from [saxon.sourceforge.net](http://saxon.sourceforge.net).


## Software required for specific transformations

Depending on the type of output that you want to generate, you might need the following applications:

-   **ICU for Java**

    ICU for Java is a cross-platform, Unicode-based, globalization library. It includes support for comparing locale-sensitive strings; formatting dates, times, numbers, currencies, and messages; detecting text boundaries; and converting character sets. You can download ICU for Java from [icu-project.org/download](http://site.icu-project.org/download).

-   **Microsoft Help Workshop**

    Required for generating HTML help. You can download the Help Workshop from [msdn.microsoft.com](http://msdn.microsoft.com/en-us/library/windows/desktop/ms669985%28v=vs.85%29.aspx).

-   **XSL-FO processor**

    Required for generating PDF output. Apache™ FOP \(Formatting Objects Processor\) is included in the distribution package. You can download other versions from [xmlgraphics.apache.org/fop](https://xmlgraphics.apache.org/fop/download.html). You can also use commercial FO processors such as Antenna House Formatter or RenderX XEP.


