# Sample JSON project files

DITA-OT includes sample project files in [JSON](https://json.org) format that can be used to define a publication project. Like the XML project samples, the sample JSON files illustrate how deliverables can be described for use in publication projects. The JSON samples are functionally equivalent to their XML and YAML counterparts, with minor adaptations to JSON file syntax.

Project files can be designed in a modular fashion to create reusable configuration structures that allow you to define settings in one file and refer to them in other projects to publish multiple deliverables at once.

For example, `*dita-ot-dir*/docsrc/samples``/project-files/html.json` defines a single HTML deliverable.

```
{
  "includes": ["common.json"],
  "deliverables": [
    {
      "name": "HTML5",
      "context": {"idref": "html"},
      "output": ".",
      "publication": {
        "transtype": "html5",
        "params": [
          {
            "name": "args.copycss",
            "value": "yes"
          },
          {
            "name": "args.css",
            "value": "dita-ot-doc.css"
          },
          {
            "name": "args.csspath",
            "value": "css"
          },
          {
            "name": "args.cssroot",
            "path": "../../resources"
          },
          {
            "name": "args.gen.task.lbl",
            "value": "YES"
          },
          {
            "name": "args.hdr",
            "href": "../../resources/header.xml"
          },
          {
            "name": "args.rellinks",
            "value": "noparent"
          },
          {
            "name": "html5.toc.generate",
            "value": "no"
          },
          {
            "name": "nav-toc",
            "value": "partial"
          }
        ]
      }
    }
  ]
}
```

This file can be used to generate the HTML version of the DITA-OT documentation by running the following command from the `docsrc` folder of the DITA-OT installation directory:

```syntax-bash
`dita` **--project**=*samples/project-files/html.json*
```

The project file for HTML output imports the common `html` context from a shared project context defined in the `*dita-ot-dir*/docsrc/samples``/project-files/common.json` file, which includes the input map file and the DITAVAL file used to filter the output.

```
{
  "contexts": [
    {
      "id": "html",
      "input": "../../userguide.ditamap",
      "profiles": {
        "ditavals": ["../../resources/html.ditaval"]
      }
    }
  ]
}
```

