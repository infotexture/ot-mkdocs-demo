# PDF customization approaches

Various methods may be used to customize the PDF output that DITA Open Toolkit produces. Each of these approaches have advantages and shortcomings that should be considered when preparing a customization project.

**Note:** Some of these methods are considered “anti-patterns” with disadvantages that outweigh their apparent appeal. In most cases, you should create a custom PDF plug-in.

## Why not edit default files?

When first experimenting with PDF customization, novice users are often tempted to simply edit the default org.dita.pdf2 files in place to see what happens.

As practical as this approach may seem, the DITA-OT project does not recommend changing any of the files in the default plug-ins.

While this method yields quick results and can help users to determine which files and templates control various aspects of PDF output, it quickly leads to problems, as any errors may prevent the toolkit from generating PDF output.

**Warning:** Any changes made in this fashion would be overwritten when upgrading to newer versions of DITA-OT, so users that have customized their toolkit installation in this way are often “stuck” on older versions of the toolkit and unable to take advantage of improvements in recent versions of DITA-OT.

## Using the Customization folder

The original Idiom plug-in used its own extension mechanism to provide overrides to the PDF transformation. With this approach, a dedicated folder within the plug-in is used to store customized files.

Files in the org.dita.pdf2/Customization folder can override their default counterparts, allowing users to adjust certain aspects of PDF output without changing any of the plug-in’s default files, or specifying additional parameters when generating output.

**Important:** While this approach is slightly better than editing default files in place, it can still cause problems when upgrading the toolkit to a new version. Since the Customization folder is located within the org.dita.pdf2 plug-in’s parent directory, users must take care to preserve the contents of this folder when upgrading to new toolkit versions.

Although recent versions of DITA-OT still support this mechanism to ensure backwards compatibility, this practice is deprecated in favor of custom PDF plug-ins.

**Tip:** Users who have used the Customization folder to modify the default PDF output are encouraged to create a custom PDF plug-in instead. In many cases, this may be as simple as copying the contents of the Customization folder to a new subfolder in the plugins folder and creating the necessary plugin.xml file and an Ant script to define the transformation type.

## Specifying an external customization directory

To ensure that overrides in customization folders are not overwritten when upgrading DITA-OT to a new release, an external customization directory can be specified at build time or in build scripts via the customization.dir parameter.

This method is preferable to the use of the org.dita.pdf2/Customization folder, as the contents of external folders are unaffected when upgrading DITA-OT. In distributed environments, users can use local installations of DITA-OT, yet still take advantage of common customizations stored in a network location available to the entire team, such as a shared drive.

It can also be useful in environments where corporate policy, CMS permissions, or network access rights prevent changes to the toolkit installation, which may prohibit the installation of custom plug-ins.

**Tip:** Users who specify external customization directories via customization.dir are encouraged to create a custom PDF plug-in if possible.

## Combining custom plug-ins &amp; customization directories

A common custom plug-in may be used to store base overrides that are applicable to all company publications, and the customization.dir parameter can be passed at build time to override individual settings as necessary for a given project or publication.

In this case, any settings in the customization directory will take precedence over their counterparts in the custom plug-in or default org.dita.pdf2 plug-in.

This approach allows a single custom plug-in to be shared between multiple publications or the entire company, without the need to create additional plug-in dependencies per project.

However, the use of multiple customization mechanisms can make it difficult to debug the precedence cascade and determine the origin of local formatting or processing overrides.

**Tip:** In most scenarios, the use of dedicated PDF customization plug-ins is preferable. Common customizations can be bundled in one plug-in, and any project-specific overrides can be maintained in separate plug-ins that build on the base branding or other settings in the common custom plug-in.

**Related information**  


[Custom PDF plug-ins](../topics/pdf-customization-plugins.md)

[PDF themes](../topics/pdf-themes.md)

