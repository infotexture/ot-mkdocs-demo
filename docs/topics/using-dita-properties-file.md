# Setting build parameters with `.properties` files

Usually, DITA builds require setting a number of parameters that do not change frequently. You can reference a set of build parameters defined in a `.properties` file when building output with the `dita` command. If needed, you can override any parameter by specifying it explicitly as an argument to the `dita` command.

## About `.properties` files

A `.properties` file is a text file that enumerates one or more name-value pairs, one per line, in the format `name = value`. The `.properties` filename extension is customarily used, but is not required.

-   Lines beginning with the `#` character are comments.
-   Properties specified as arguments of the `dita` command override those set in `.properties` files.

    **Restriction:** For this reason, **args.input** and **transtype** can’t be set in the `.properties` file.

-   If you specify the same property more than once, the last instance is used.
-   Properties not used by the selected transformation type are ignored.
-   Properties can reference other property values defined elsewhere in the `.properties` file or passed by the `dita` command. Use the Ant `${*property.name*}` syntax.
-   You can set properties not only for the default DITA-OT transformation types, but also for custom plugins.

1.  Create your `.properties` file.

    **Tip:** Copy `*dita-ot-dir*/docsrc/samples``/properties/template.properties`; this template describes each of the properties you can set.

    For example:

    ```
    # Directory that contains the custom .css file:
    args.cssroot = ${args.input.dir}/css/
    
    # Custom .css file used to style output:
    args.css = style.css
    
    # Copy the custom .css file to the output directory:
    args.copycss = yes
    
    # Location of the copied .css file relative to the output:
    args.csspath = branding
    
    # Generate a full navigation TOC in topic pages:
    nav-toc = full
    ```

2.  Reference your `.properties` file with the `dita` command when building your output.

    ```syntax-bash
    `dita` **--input**=*my.ditamap* **--format**=html5 **--propertyfile**=*my.properties*
    ```

3.  If needed, pass additional arguments to the `dita` command to override specific build parameters.

    For example, to build output once with `<draft>` and `<required-cleanup>` content:

    ```syntax-bash
    `dita` **--input**=*my.ditamap* **--format**=html5 **--propertyfile**=*my.properties* \
         **--args.draft**=yes
    ```

    **Tip:** If you are building in different environments where the location of the input files is not consistent, set args.input.dir with the `dita` command and reference its value with `${args.input.dir}` in your `.properties` file.


