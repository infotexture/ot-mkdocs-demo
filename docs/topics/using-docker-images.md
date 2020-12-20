# Running the dita command from a Docker image

[Docker](https://www.docker.com) is a platform used to build, share, and run portable application containers. As of version 3.4, the DITA-OT project provides an official Docker container image that includes everything you need to run the toolkit and publish DITA content from a containerized environment.

## About application containers

Using containers to deploy applications isolates software from its environment to ensure that it works consistently despite any differences in the host operating system, for example.

Docker containers are designed as stateless machines that can be quickly created and destroyed, started and stopped. Each Docker image provides its own private filesystem that includes only the code required to run the application itself — it is not intended for persistent data storage.

When a container is stopped, any changes made within the container are lost, so source files and generated output should be stored outside the container. These resources are attached to the container by mounting directories from the host machine.

To run the DITA-OT image, you will need to install Docker and log in to the GitHub Package Registry.

-   To download Docker Desktop, you may be prompted to sign in with your Docker ID \(or sign up to create one\).
-   To retrieve docker images from the GitHub Package Registry, you will also need a GitHub account.

1.  Install Docker for your operating system.

    -   [Install Docker Desktop on Windows](https://docs.docker.com/docker-for-windows/install/)
    -   [Install Docker Desktop on Mac](https://docs.docker.com/docker-for-mac/install)
    -   On macOS, you can also install Docker Desktop via [Homebrew](https://brew.sh):

        ```syntax-bash
        $ brew cask install docker
        Downloading…
        ```

    -   On Linux, install Docker Community Edition \(CE\) via your operating system’s package manager, for example:

        ```syntax-bash
        $ sudo apt-get install docker-ce
        ```

2.  Log in to the GitHub Package Registry.

    1.  In your [GitHub profile settings](https://github.com/settings/tokens), create a new personal access token with the `read:packages` and `repo` scopes.

        For more information, see [Creating a personal access token for the command line](https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line).

    2.  On the command line, run the docker command to log in with your GitHub credentials.

        ```syntax-bash
        docker login docker.pkg.github.com -u USERNAME -p PASSWORD/TOKEN
        ```

        For more information, see [Authenticating to GitHub Package Registry](https://help.github.com/en/articles/configuring-docker-for-use-with-github-package-registry#authenticating-to-github-package-registry).

3.  To build output, map a host directory to a container volume and specify options for the dita command.

    ```syntax-bash
    $ docker run -it \
      -v /Users/username/source:/src docker.pkg.github.com/dita-ot/dita-ot/dita-ot:3.6 \
      -i /src/input.ditamap \
      -o /src/out \
      -f html5 -v
    ```

    This command sequence specifies the following options:

    -   -v mounts the source subfolder of your home directory and binds it to the /src volume in the container
    -   -i specifies the input.ditamap file in your source folder as the input map file
    -   -o writes the output to source/out
    -   -f sets the output format to HTML5, and
    -   -v displays build progress messages with verbose logging
    On Windows, if your Users directory is on the C:\\ drive, use /c/Users/… to map the host directory:

    ```
    > C:\Users\username> docker run -it ^
      -v /c/Users/username/source:/src docker.pkg.github.com/dita-ot/dita-ot/dita-ot:3.6 ^
      -i /src/input.ditamap ^
      -o /src/out ^
      -f html5 -v
    ```

    **Note:** The DITA-OT container image uses the `ENTRYPOINT` instruction to run the dita command from the /opt/app/bin/ directory of the container automatically, so you there’s no need to include the dita command itself, only the arguments and options you need to publish your content.


**Related information**  


[Using the Open Toolkit Through Docker Containers](https://www.oxygenxml.com/events/2016/dita-ot_day.html#Using_the_Open_Toolkit_Through_Docker_Containers)

