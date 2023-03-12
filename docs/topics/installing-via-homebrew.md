# Installing DITA-OT via Homebrew

An alternative installation method can be used to install DITA-OT via [Homebrew](https://brew.sh), one of the most popular open-source package managers on macOS and Linux.

The steps below assume you have already installed [Homebrew](https://brew.sh) according to the instructions at [brew.sh](https://brew.sh).

**Tip:** Verify that your [PATH environment variable](https://en.wikipedia.org/wiki/PATH_(variable)) begins with the bin subfolder of the Homebrew installation directory [1](#fntarg_1) to ensure that Homebrew-installed software takes precedence over any programs of the same name elsewhere on the system.

1.  Update Homebrew to make sure the latest package formulas are available on your system:

    ```syntax-bash
    $ brew update
    Already up-to-date.
    ```

    Homebrew responds with a list of any new or updated formulæ.

2.  Check the version of DITA-OT that is available from Homebrew:

    ```syntax-bash
    $ brew info dita-ot
    dita-ot: stable 4.0.2
    DITA Open Toolkit is an implementation of the OASIS DITA specification
    https://www.dita-ot.org/
    /opt/homebrew/Cellar/dita-ot/4.0.2 \(number of files, package size\) \*
      Poured from bottle using the formulae.brew.sh API on YYYY-MM-DD at hh:mm:ss
    From: https://github.com/Homebrew/homebrew-core/blob/master/Formula/dita-ot.rb
    License: Apache-2.0
    ==&gt; Dependencies
    Required: openjdk ✔
    
    ```

    The version of the DITA-OT formula is shown, along with basic information on the package.

3.  Install the `dita-ot` package:

    ```syntax-bash
    $ brew install dita-ot
    Downloading…
    ```

    Homebrew will automatically download the latest version of the toolkit, install it in a subfolder of the local package Cellar and symlink the dita command to the bin subfolder of the Homebrew installation directory.

4.  Verify the installation:

    ```syntax-bash
    $ which dita
    /opt/homebrew/bin/dita
    ```

    The response confirms that the system will use the Homebrew-installed version of DITA-OT.

5.  Check the DITA-OT version number:

    ```syntax-bash
    $ dita --version
    DITA-OT version 4.0.2
    ```

    The DITA-OT version number appears on the console.


You can now run the dita command to transform DITA content.

**Related information**  


[Installing DITA-OT on macOS via Homebrew](https://www.oxygenxml.com/events/2018/dita-ot_day.html#installing_DITA-OT_on_macOS_via_homebrew)

[1](#fnsrc_1) Homebrew’s default installation location depends on the operating system architecture: -   /usr/local on macOS Intel
-   /opt/homebrew on macOS ARM
-   /home/linuxbrew/.linuxbrew on Linux



