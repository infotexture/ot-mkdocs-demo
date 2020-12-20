# Installing plug-ins in a Docker image

To install custom plug-ins or make other changes based on the DITA-OT parent image, you can create your own Dockerfile and specify the official DITA-OT image as the basis for your image.

Each subsequent declaration in the Dockerfile modifies this parent image, so you can start with the official image, and add custom plug-ins or other commands as required to create a custom Docker image that includes everything you need to publish your content.

1.  Create a new Dockerfile and specify the official DITA-OT image in the FROM directive.

    ```
    # Use the latest official DITA-OT image as parent:   ↓
    FROM docker.pkg.github.com/dita-ot/dita-ot/dita-ot:3.6
    ```

2.  You can extend your image with a `RUN` declaration that runs the dita command from the container to install a custom plug-in, and specify the filename or URL of the plug-in’s distribution ZIP file.

    ```
    # Install a custom plug-in from a remote location:
    RUN dita --install https://github.com/infotexture/dita-bootstrap/archive/3.4.1.zip
    ```

3.  You can also install custom plug-ins from the main DITA-OT plug-in registry at [dita-ot.org/plugins](https://www.dita-ot.org/plugins), or from your company plug-in registry.

    ```
    # Install from the registry at dita-ot.org/plugins:
    RUN dita --install org.dita-community.pdf-page-break
    ```


The docsrc/samples folder in the DITA-OT installation directory contains a complete example:

```
# Use the latest official DITA-OT image as parent:   ↓
FROM docker.pkg.github.com/dita-ot/dita-ot/dita-ot:3.6

# Install a custom plug-in from a remote location:
RUN dita --install https://github.com/infotexture/dita-bootstrap/archive/3.4.1.zip

# Install from the registry at dita-ot.org/plugins:
RUN dita --install org.dita-community.pdf-page-break
```

## Building a new image

You can build a Docker image from this example by running the following command from the dita-ot-dir/docsrc/samples directory:

```syntax-bash
$ docker image build -t sample-docker-image:1.0 .
Sending build context to Docker daemon  2.048kB
Step 1/3 : FROM docker.pkg.github.com/dita-ot/dita-ot/dita-ot:3.6
 ---> 9abb96827538
Step 2/3 : RUN dita --install https://github.com/infotexture/dita-bootstrap/archive/3.4.1.zip
 ---> Running in d510f874cae0
Added net.infotexture.dita-bootstrap
Removing intermediate container d510f874cae0
 ---> 63deb8e15b5b
Step 3/3 : RUN dita --install org.dita-community.pdf-page-break
 ---> Running in b4ef2fcad916
Added org.dita-community.pdf-page-break
Removing intermediate container b4ef2fcad916
 ---> 402885636b7f
Successfully built 402885636b7f
Successfully tagged sample-docker-image:1.0

```

Docker steps through each instruction in the Dockerfile to build the sample image. In this case, the dita command provides feedback on each installed plug-in.

## Running the new container

You can then start a container based on your new image:

```syntax-bash
$ docker container run -it \
  -v /path/to/dita-ot-dir/docsrc:/src sample-docker-image:1.0 \
  -i /src/userguide.ditamap \
  -o /src/out/dita-bootstrap \
  -f html5-bootstrap -v
```

This command sequence specifies the following options:

-   -v mounts the docsrc subfolder of the DITA-OT directory on your host machine and binds it to the /src volume in the container
-   -i specifies dita-ot-dir/docsrc/userguide.ditamap as the input map file
-   -o writes the output to dita-ot-dir/docsrc/out/dita-bootstrap
-   -f sets the output format to the Bootstrap template, and
-   -v displays build progress messages with verbose logging

When the build is finished, you should find a copy of the DITA-OT documentation under dita-ot-dir/docsrc/out/dita-bootstrap, styled with the basic Bootstrap template from the custom plug-in.

