# Publishing with project files

DITA-OT 3.4 introduces new project files to define publication projects with multiple deliverables. Projects specify a context, output folder, and publication for each deliverable. A re-usable context groups source files and filters, and a publication defines an output format with transformation parameters. You can pass a project file to the dita command to publish multiple deliverables at once.

## About project files

Project files may be defined in one of three formats: XML, [JSON](https://json.org), or [YAML](https://yaml.org). The XML format can be validated with a RELAX NG schema provided in the resources folder of the DITA-OT installation \(project.rnc\).

**Note:** The XML project file format is the normative version provided for interoperability with existing XML-based toolchains. The JSON and YAML versions are alternative compact formats that are easier to read and write, but otherwise equivalent to the XML syntax.

Whereas .properties files can only be used to set parameters, project files go further, allowing you to define multiple deliverables with separate input files and output folders and formats for each publication. A project file can also refer to other project files, so you can re-use common configuration structures across projects.

Another advantage of project files over .properties files is that they allow you to specify paths relative to the project file, even for parameters that require absolute paths, such as:

-   `args.cssroot`
-   `args.ftr`
-   `args.hdf`
-   `args.hdr`

Though the exact syntax differs slightly, the basic structure of project files is similar in all supported formats.

-   You can link to other project files with `include(s)`

-   Projects can define multiple `deliverables`, which consist of:

    -   a publication `context` that may include:

        -   an `id` used to refer to this context from other projects
        -   a series of `input` files \(DITA maps\)
        -   a `profile` with a series of DITAVAL files used to filter the content
    -   an `output` location \(relative to the CLI --output directory\)

    -   a `publication` that defines:
        -   an output format via `transtype`, and
        -   a series of parameters to set for this transformation type, specified via `name` and either `href`, `path`, or `value`

**Tip:**

-   Use `href` for web addresses and other resources that should resolve to an absolute URI.
-   Use `path` for parameters that require an absolute value, like args.cssroot. Paths may be defined relative to the project file, but are always expanded to an absolute system path.
-   Use `value` to define strings and relative values for properties like args.csspath, which is used to describe a relative path in the output folder.

1.  Create a project file to define the deliverables in your publication project.

    For example:

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <?xml-model href="https://www.dita-ot.org/rng/project.rnc" type="application/relax-ng-compact-syntax"?>
    <project xmlns="https://www.dita-ot.org/project">
      <deliverable id="pdf">
        <context name="User Guide">
          <input href="../../userguide-book.ditamap"/>
        </context>
        <output href="."/>
        <publication transtype="pdf2">
          <param name="args.chapter.layout" value="BASIC"/>
          <param name="args.gen.task.lbl" value="YES"/>
          <param name="include.rellinks" value="friend"/>
          <param name="outputFile.base" value="userguide"/>
          <param name="processing-mode" value="strict"/>
        </publication>
      </deliverable>
    </project>
    ```

2.  Pass your project file to the dita command to build output.

    ```syntax-bash
    dita --project=pdf.xml
    ```

3.  If needed, pass additional arguments to the dita command to override specific build parameters.

    For example, to build output once with `draft` and `required-cleanup` content:

    ```syntax-bash
    dita --project=pdf.xml --args.draft=yes
    ```

4.  If your project contains multiple deliverables, you can pass the --deliverable option to generate output for a single deliverable ID.

    ```syntax-bash
    dita --project=all.xml --deliverable=htmlhelp
    ```


**Related information**  


[Editing DITA Open Toolkit Project files](https://www.oxygenxml.com/events/2019/dita-ot_day.html#editing_dita_open_toolkit_project_files)

[One file to rule them all \(DITA Project\)](https://www.oxygenxml.com/events/2019/dita-ot_day.html#one_file_to_rule)

