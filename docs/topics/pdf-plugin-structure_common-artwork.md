# Custom artwork

The common/artwork folder houses custom artwork files that override the standard icons in org.dita.pdf2/cfg/common/artwork.

These files are used to graphically identify different types of DITA `note` element.

The mapping between `note` type and graphic is contained in the common variables file org.dita.pdf2/cfg/common/vars/commonvariables.xml.

The variables that control `note` graphics all follow the form

```language-xml
<variable id="\{type\} Note Image Path"> \{path to image file\} </variable>
```

where \{type\} contains a possible value for the `note` `@type` attribute and \{path to image file\} is the path to the note icon image.

