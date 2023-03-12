# Sample XML project files

DITA-OT includes sample XML project files that can be used to define a publication project. The XML format can be validated with a RELAX NG schema provided in the resources folder of the DITA-OT installation \(project.rnc\).

Project files can be designed in a modular fashion to create reusable configuration structures that allow you to define settings in one file and refer to them in other projects to publish multiple deliverables at once.

For example, dita-ot-dir/docsrc/samples/project-files/html.xml defines a single HTML deliverable.

```
<?xml version="1.0" encoding="UTF-8"?>
<?xml-model href="https://www.dita-ot.org/rng/project.rnc" type="application/relax-ng-compact-syntax"?>
<project xmlns="https://www.dita-ot.org/project">
  <include href="common.xml"/>
  <deliverable name="HTML5" id="html">
    <context idref="html"/>
    <output href="."/>
    <publication transtype="html5">
      <param name="args.copycss" value="yes"/>
      <param name="args.css" value="dita-ot-doc.css"/>
      <param name="args.csspath" value="css"/>
      <param name="args.cssroot" path="../../resources"/>
      <param name="args.gen.task.lbl" value="YES"/>
      <param name="args.hdr" href="../../resources/header.xml"/>
      <param name="html5.toc.generate" value="no"/>
      <param name="nav-toc" value="partial"/>
      <param name="processing-mode" value="strict"/>
    </publication>
  </deliverable>
</project>
```

This file can be used to generate the HTML version of the DITA-OT documentation by running the following command from the docsrc folder of the DITA-OT installation directory:

```
dita --project=samples/project-files/html.xml
```

The project file for HTML output imports the common `html` context from a shared project context defined in the dita-ot-dir/docsrc/samples/project-files/common.xml file, which includes the input map file and the DITAVAL file used to filter the output.

```
<?xml version="1.0" encoding="UTF-8"?>
<?xml-model href="https://www.dita-ot.org/rng/project.rnc" type="application/relax-ng-compact-syntax"?>
<project xmlns="https://www.dita-ot.org/project">
  <context id="html" name="HTML">
    <input href="../../userguide.ditamap"/>
    <profile>
      <ditaval href="../../resources/html.ditaval"/>
    </profile>
  </context>
</project>
```

The same common `html` context is also referenced in the project file for HTMLHelp output, as illustrated in dita-ot-dir/docsrc/samples/project-files/htmlhelp.xml.

```
<?xml version="1.0" encoding="UTF-8"?>
<?xml-model href="https://www.dita-ot.org/rng/project.rnc" type="application/relax-ng-compact-syntax"?>
<project xmlns="https://www.dita-ot.org/project">
  <deliverable name="HTMLHelp" id="htmlhelp">
    <context idref="html"/>
    <output href="htmlhelp"/>
    <publication transtype="htmlhelp">
      <param name="args.copycss" value="yes"/>
      <param name="args.css" value="dita-ot-doc.css"/>
      <param name="args.csspath" value="css"/>
      <param name="args.cssroot" path="../../resources"/>
      <param name="args.gen.task.lbl" value="YES"/>
      <param name="processing-mode" value="strict"/>
    </publication>
  </deliverable>
</project>
```

The dita-ot-dir/docsrc/samples/project-files/pdf.xml file defines a single PDF deliverable.

```
<?xml version="1.0" encoding="UTF-8"?>
<?xml-model href="https://www.dita-ot.org/rng/project.rnc" type="application/relax-ng-compact-syntax"?>
<project xmlns="https://www.dita-ot.org/project">
  <deliverable id="pdf">
    <context name="User Guide">
      <input href="../../userguide-book.ditamap"/>
      <profile>
        <ditaval href="../../resources/pdf.ditaval"/>
      </profile>
    </context>
    <output href="."/>
    <publication transtype="pdf2">
      <param name="args.chapter.layout" value="BASIC"/>
      <param name="args.gen.task.lbl" value="YES"/>
      <param name="include.rellinks" value="#default external"/>
      <param name="outputFile.base" value="userguide"/>
      <param name="processing-mode" value="strict"/>
      <param name="theme" path="../themes/dita-ot-docs-theme.yaml"/>
    </publication>
  </deliverable>
</project>
```

This file can be used to generate the PDF version of the DITA-OT documentation by running the following command from the docsrc folder of the DITA-OT installation directory:

```
dita --project=samples/project-files/pdf.xml
```

The dita-ot-dir/docsrc/samples/project-files/distribution-docs.xml file includes both the HTML and PDF projects as follows:

```
<project xmlns="https://www.dita-ot.org/project">
  <include href="html.xml"/>
  <include href="pdf.xml"/>
</project>
```

To build both the HTML and PDF versions of the documentation as included in the distribution package, run the following command from the docsrc folder of the DITA-OT installation directory:

```
dita --project=samples/project-files/distribution-docs.xml
```

The dita-ot-dir/docsrc/samples/project-files/all.xml file includes all three project deliverables as follows:

```
<project xmlns="https://www.dita-ot.org/project">
  <include href="html.xml"/>
  <include href="htmlhelp.xml"/>
  <include href="pdf.xml"/>
</project>
```

