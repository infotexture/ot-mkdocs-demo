# Glossary

Certain terms have particular meaning in the context of the DITA Open Toolkit project.

## argument

Required parameter passed to the Ant process or dita command.

## DITA Open Toolkit

The open-source publishing engine for content authored in the Darwin Information Typing Architecture.

### DITA-OT

**Note:** Treat as a proper noun; do not precede with *the* definite article.

### DOST

**Note:** Deprecated acronym for “**D**ITA **O**pen *__S__ource* **T**oolkit”. Use DITA-OT instead.

## extension point

Pre-defined interface that can be added to a plug-in to allow other plug-ins to extend or customize portions of its functionality. An extendable feature is defined by declaring an `extension-point` element in the plugin.xml file. Other plug-ins can then override the default behavior by defining custom code that runs when this extension point is called.

## option

Discretionary parameter passed to the Ant process or dita command.

## output format

Deliverable file or set of files containing all of the transformed content.

## parameter

Command-line argument or option passed to the Ant process or dita command.

## plug-in

Group of related files that change the default behavior of DITA-OT in some way.

## processor

Software that performs a series of operations to transform DITA content from one format to another.

## property

Ant-specific argument or option.

## template

Optional `template` elements can be added to plugin.xml files to define XML or XSL files that integrate DITA-OT extensions. Template files are often named with a \_template suffix, and may be used to create custom extensions, group targets, and more. Anything contained in the plug-in’s template files is integrated when the plug-in is installed.

## transformation type

Component of a plug-in that defines an output format.

### transtype

**Note:** Abbreviated form of transformation type. Use only to refer to the transtype parameter of the dita command, or to the `transtype` element in a plugin.xml file that defines the output format.

## variable

Language-specific piece of generated text, most often defined in the files in org.dita.base\\xsl\\common.

## XSL template

Set of rules in an XSL stylesheet that are applied to nodes that match specific XML structures.

