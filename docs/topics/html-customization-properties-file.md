# Customizing HTML with a `.properties` file

You can also use a `.properties` file to reference a set of build parameters when building output with the `dita` command. The DITA-OT documentation uses a `.properties` file to include custom CSS, header branding, and table-of-contents navigation in the HTML5 output.

1.  Create a `.properties` file to store the parameter settings for your customization.

    **Tip:** You can use one of the sample `.properties` files from the DITA-OT documentation as a starting point for your own customizations. These files are available in the installation folder under `docsrc/samples/properties/`.

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


**Note:** For an example of HTML output generated using this method, see the HTML5 version of the DITA-OT documentation included in the installation folder under `doc/index.html`.

