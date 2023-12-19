# Installing DITA Open Toolkit

The DITA-OT distribution package can be installed on Linux, macOS, and Windows. It contains everything that you need to run the toolkit except for Java.

-   Ensure that you have a Java Runtime Environment \(JRE\) or Java Development Kit \(JDK\).

    DITA-OT 4.1 is designed to run on Java version 17 or later and built and tested with the Open Java Development Kit \(OpenJDK\). Compatible Java distributions are available from multiple sources:

    -   You can download the Oracle JRE or JDK from [oracle.com/java](https://www.oracle.com/java/technologies/downloads/) under commercial license.
    -   Eclipse Temurin is the free OpenJDK distribution available from [adoptium.net](https://adoptium.net/temurin/releases/?version=17).
    -   Free OpenJDK distributions are also provided by [Amazon Corretto](https://aws.amazon.com/corretto/), [Azul Zulu](https://www.azul.com/downloads/), and [Red Hat](https://developers.redhat.com/products/openjdk/download).
-   If you want to generate HTML Help, ensure that you have HTML Help Workshop installed.

    You can download the Help Workshop from [msdn.microsoft.com](http://msdn.microsoft.com/en-us/library/windows/desktop/ms669985%28v=vs.85%29.aspx).


1.  Download the `dita-ot-4.1.2.zip` package from the project website at [dita-ot.org/download](https://www.dita-ot.org/download).

2.  Extract the contents of the package to the directory where you want to install DITA-OT.

3.  Add the absolute path for the `bin` folder of the DITA-OT installation directory to the [PATH environment variable](https://en.wikipedia.org/wiki/PATH_(variable)).

    **Tip:** This defines the necessary environment variable that allows the `dita` command to be run from any location on the file system without typing the path to the command.


