# The plugin.properties file

The plugin.properties file is used to store configuration properties that are set by the plug-in installation process.

The file is located in the lib/org.dita.dost.platform directory of the DITA-OT installation and stores a cached version of the plug-in configuration used by the Java code.

The contents of this file depend on the installed plug-ins. Each plug-in may contribute properties such as the path to the plug-in folder, supported extensions and print transformation types.

**Warning:** The plugin.properties file is regenerated each time the plug-in integration process is run, so it should not be edited manually as these changes would be lost the next time a plug-in is installed or removed.

