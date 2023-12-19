# Publishing with project files

DITA-OT 3.4 introduced project files that allow you to publish multiple deliverables at once. Each deliverable specifies a re-usable source `context` that groups the maps or topics you want to publish, an `output` folder, and a `publication` format \(such as HTML, or PDF\) with transformation parameters.

## About project files

Project files may be defined in one of three formats: XML, [JSON](https://json.org), or [YAML](https://yaml.org). The XML format can be validated with a RELAX NG schema provided in the `resources` folder of the DITA-OT installation \(`project.rnc`\).

**Note:** The XML project file format is the normative version provided for interoperability with existing XML-based toolchains. The JSON and YAML versions are alternative compact formats that are easier to read and write, but otherwise equivalent to the XML syntax.

Whereas `.properties` files can only be used to set parameters, project files go further, allowing you to define multiple deliverables with separate input files and output folders and formats for each publication. A project file can also refer to other project files with `include` statements. Deliverables, contexts, and publications can either be entirely self-contained, or reference others with `idref` attributes, so you can re-use common configuration structures across \(and within\) projects.

Another advantage of project files over `.properties` files is that they allow you to specify paths relative to the project file, even for parameters that require absolute paths, such as:

-   `args.cssroot`
-   `args.ftr`
-   `args.hdf`
-   `args.hdr`

## Syntax

Though the exact syntax differs slightly, the basic structure of project files is similar in all supported formats.

The following settings can be defined for each `deliverable`:

-   a source `context` that may include:

    -   an `id` that allows you to refer to this context from other contexts or projects
    -   an `idref` that refers to another context
    -   a series of `input` files \(the DITA maps or topics you want to publish\)
    -   a `profile` with a series of DITAVAL files used to filter the content of all publications in the deliverable
-   an `output` location \(relative to the CLI **--output** directory\)

-   a `publication` type that defines:

    -   an `id` that allows you to refer to this publication from other publications or projects
    -   an `idref` that refers to another publication
    -   a `transtype` that specifies an output format \(such as HTML, or PDF\)
    -   a series of `param` elements, with any parameters to set for this transformation type, specified via `name` and either `href`, `path`, or `value`
    -   a `profile` with any additional DITAVAL files used to filter the content of the publication \(in addition to any filters defined in the map context\)
    Parameters defined in a publication can override those in other publications that are referenced via `idref`.

    ```
    <project xmlns="https://www.dita-ot.org/project">
      <publication transtype="html5" id="common-html5">
        <param name="nav-toc" value="partial"/>
      </publication>
      <deliverable>
        <context>
          <input href="root.ditamap"/>
        </context>
        <output href="./out"/>
        <publication idref="common-html5">
          <param name="nav-toc" value="full"/> <!-- override common HTML publication -->
        </publication>
      </deliverable>
    </project>
    ```


**Tip:**

-   Use `href` for web addresses and other resources that should resolve to an absolute URI. Relative references are resolved using the project file as a base directory.
-   Use `path` for parameters that require an absolute value, like **args.cssroot**. Paths may be defined relative to the project file, but are always expanded to an absolute system path.
-   Use `value` to define strings and relative values for properties like **args.csspath**, which is used to describe a relative path in the output folder. String values are passed as is.

## Project filtering

As of DITA-OT 4.0, you can add DITAVAL filters to both contexts and publications. If a set of filter conditions applies to most or all of your deliverables, then it should probably be defined in a publication, rather than in contexts.

For example, consider a case with 100 maps that have multiple `@product` variants, but every one of which is published in two `@audience` conditions \(internal or external\). If `@audience` is varied in publications, the structure is orthogonal and well-organized:

![](../reference/images/sample-project-filtering-scenario.svg "Sample filtering scenario")

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
          <param name="include.rellinks" value="#default external"/>
          <param name="outputFile.base" value="userguide"/>
          <param name="theme" path="../themes/dita-ot-docs-theme.yaml"/>
          <profile>
            <ditaval href="../../resources/pdf.ditaval"/>
          </profile>
        </publication>
      </deliverable>
    </project>
    ```

2.  Pass your project file to the `dita` command to build output.

    ```syntax-bash
    `dita` **--project**=*pdf.xml*
    ```

3.  If needed, pass additional arguments to the `dita` command to override specific build parameters.

    For example, to build output once with `<draft>` and `<required-cleanup>` content:

    ```syntax-bash
    `dita` **--project**=*pdf.xml* **--args.draft**=yes
    ```

4.  If your project contains multiple deliverables, you can pass the **--deliverable** option to generate output for a single deliverable ID.

    ```syntax-bash
    `dita` **--project**=*all.xml* **--deliverable**=htmlhelp
    ```


**Related information**  


[Editing DITA Open Toolkit Project files](https://www.oxygenxml.com/events/2019/dita-ot_day.html#editing_dita_open_toolkit_project_files)

[One file to rule them all \(DITA Project\)](https://www.oxygenxml.com/events/2019/dita-ot_day.html#one_file_to_rule)

