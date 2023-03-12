# Adding custom CSS

To modify the appearance of the default HTML output that DITA Open Toolkit generates, you can reference a custom Cascading Style Sheet \(CSS\) file with the typography, colors, and other presentation aspects that define your corporate identity.

You can use this approach when you need to adjust the look and feel of the default output for a single project, but don’t want to create a custom DITA-OT plug-in.

You can version the CSS file along with the DITA source files in your project, so stylesheet changes can be tracked along with modifications to topic content.

You may also find this approach useful as you develop a custom stylesheet. Once the CSS rules stabilize, you can bundle the CSS file in a custom DITA-OT plug-in to ensure consistent HTML output across projects.

1.  Create a custom CSS file and store it in your project along with your DITA source files.

    **Note:** As a starting point, you can use the CSS file that is used for the DITA-OT documentation. This file is available in the installation folder under docsrc/resources/dita-ot-doc.css.

2.  Set the args.css parameter to the name of your custom CSS file.

    The value of this parameter should be only the file name. You can specify the absolute path to the file with args.cssroot.

3.  Set the args.copycss parameter to yes.

    This setting ensures that your custom CSS file will be copied to the output directory.

4.  Set args.cssroot to the absolute path of the folder that contains your custom CSS file.

5.  Set args.csspath to specify the location of the CSS file in the output folder.

    If args.csspath is not set, the custom CSS file will be copied to the root level of the output folder. To copy the CSS file to a subfolder named css, set args.csspath to css.


**Tip:** For an example of HTML output generated using this method, see the HTML5 version of the DITA-OT documentation included in the installation folder under doc/index.html.

**Related information**  


[Bundling CSS in a custom HTML plug-in](../topics/html-customization-plugin-bundle-css.md)

