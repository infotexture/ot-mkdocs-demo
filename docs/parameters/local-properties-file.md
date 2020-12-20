# The local.properties file

A local.properties file in the root directory of the DITA-OT installation can be used to override the default values of various DITA-OT parameters.

For example, if you always use the same rendering engine to produce PDF output for all of your projects, you could create a local.properties file in the root directory of your DITA-OT installation to set the pdf.formatter parameter and additional options for the XSL processor:

```
# Use RenderX XEP Engine for PDF output
pdf.formatter = xep

# Specify the user configuration file for RenderX
custom.xep.config = /path/to/custom.config
```

Backslash “\\” characters in .properties files must be escaped with a second backslash as “\\\\”. If you use Antenna House Formatter on a Windows system, for example, you would set the path to the command using a properties file entry like this:

```
# Use Antenna House Formatter for PDF output
pdf.formatter = ah

# Specify the path to the Antenna House Formatter command
axf.cmd=C:\\Program Files\\Antenna House\\AHFormatterV62
```

**Note:** This file can only be used to set Ant property values that can be passed as argument parameters to the command line. The DITA-OT Java code does not read this file.

