# Running the dita command from a GitHub Action

[GitHub Actions](https://github.com/features/actions) are a CI/CD workflow mechanism attached to GitHub. Each action is an individual unit of functionality that can be combined with other GitHub Actions to create workflows, which are triggered in response to certain GitHub events. As of version 3.6.1, the DITA-OT project provides an official [dita-ot-action](https://github.com/dita-ot/dita-ot-action) that can be used as a step within a GitHub workflow to publish documentation as part of your CI/CD pipeline.

## About GitHub Actions

GitHub Actions can automate tasks such as document generation as part of your software development life cycle. GitHub Actions are event-driven, allowing a series of tasks to run one after another when a specified event has occurred.

Each step is an individual atomic task that can run commands in a job. A step can be either an action or a shell command. Each step in a job executes on the same runner, allowing the actions in that job to share data with each other, therefore files generated through the `dita-ot-build` action can be archived or published by later actions within the same job.

1.  In your GitHub repository, create the `.github/workflows/` directory to store your workflow files.

2.  In the `.github/workflows/` directory, create a new file called dita-ot-build-actions.yml and add the following code.

    ```
    name: CI
    'on':
      push:
        branches:
          - master
    jobs:
      build-dita:
        name: Build DITA
        runs-on: ubuntu-latest
        steps:
          - name: Git checkout
            uses: actions/checkout@v2
    ```

    This setup ensures the action runs whenever code is updated on the `master` branch and checks out the codebase.

3.  In the same file, add the following code.

    ```
          - name: Build PDF
            uses: dita-ot/dita-ot-action@master
            with:
              input: document.ditamap
              transtype: pdf
              output-path: out
    ```

    This action specifies the following:

    -   name defines the name of the action to be displayed within the GitHub repository
    -   uses specifies the name and version of the GitHub Action to run. Use `dita-ot/dita-ot-action@master` to run the latest version.
    -   input specifies the name and location of the input map file within the GitHub repository \(relative to the repository root\)
    -   transtype sets the output format to PDF, and
    -   output-path writes the output to the out folder within the running action

The docsrc/samples folder in the DITA-OT installation directory contains several complete examples. The following GitHub Action generates styled HTML and PDF outputs.

```
name: CI
'on':
  push:
    branches:
      - master
jobs:
  build-dita:
    name: Build DITA
    runs-on: ubuntu-latest
    steps:
      - name: Git checkout
        uses: actions/checkout@v2
      - name: Build HTML5 + Bootstrap
        uses: dita-ot/dita-ot-action@master
        with:
          plugins: |
            net.infotexture.dita-bootstrap
          input: document.ditamap
          transtype: html5-bootstrap
          output-path: out

      - name: Build PDF
        uses: dita-ot/dita-ot-action@master
        with:
          install: |
            # Run some arbitrary installation commands
            apt-get update -q
            apt-get install -qy --no-install-recommends nodejs
            nodejs -v

            # Install plugins
            dita install fox.jason.extend.css
            dita install org.doctales.xmltask
            dita install fox.jason.prismjs
          build: |
            # Use the dita command line
            dita -i document.ditamap -o out -f pdf --filter=filter1.ditaval

      - name: Upload DITA Output to a ZIP file
        uses: actions/upload-artifact@v2
        with:
          name: dita-artifact
          path: 'out'

      - name: Deploy DITA Output to GitHub Pages
        uses: JamesIves/github-pages-deploy-action@3.7.1
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          BRANCH: gh-pages # The branch the action should deploy to.
          FOLDER: out # The folder the action should deploy.
```

The **Build HTML5 + Bootstrap** step reuses the input, transtype and output-path settings. In addition, additional DITA-OT plug-ins can be loaded using the plugins parameter, with each plug-in separated by a comma or new line separator.

The **Build PDF** step uses an alternative syntax where the install and build parameters are used to run arbitrary commands from the command line.

See the docsrc/samples/github-actions folder in the DITA-OT installation directory for additional examples of GitHub Actions for different scenarios.

