# Adding plug-ins via the registry

DITA-OT 3.2 supports a new plug-in registry that makes it easier to discover and install new plug-ins. The registry provides a searchable list of plug-ins at [dita-ot.org/plugins](https://www.dita-ot.org/plugins).

In the past, installing plug-ins required you to either download a plug-in to your computer and provide the path to the plug-in archive \(.zip file\) or pass the URL of the plug-in distribution file to the dita command and let DITA-OT download the file. This required that you know the URL of the plug-in distribution package.

## Installing plug-ins from the registry

With the registry, you can now search the list of available plug-ins at [dita-ot.org/plugins](https://www.dita-ot.org/plugins) and install new plug-ins by name and optional version.

Search the registry for a plug-in and install it by providing the plug-in name to the dita command.

```syntax-bash
dita --install=<plugin-name\>
```

If the registry includes multiple versions of the same plug-in, you can specify the version to install as follows:

```syntax-bash
dita --install=<plugin-name\>@<plugin-version\>
```

If the plug-in requires other plug-ins, those are also installed recursively.

For example, to revert PDF output to the legacy PDF2 layout that was the default in DITA-OT before 2.5, install the org.dita.pdf2.legacy plug-in as follows:

```syntax-bash
dita --install=org.dita.pdf2.legacy
```

If a matching plug-in cannot be found, an error message will appear. Possible reasons for failure include:

-   A plug-in with the specified name was not found in the registry
-   A plug-in with the specified version was not found in the registry
-   The specified plug-in version is not compatible with the installed DITA-OT version
-   None of the available plug-in versions are compatible with the installed DITA-OT version

## Publishing plug-ins to the registry

The contents of the DITA Open Toolkit plug-in registry are stored in a Git repository at [github.com/dita-ot/registry](https://github.com/dita-ot/registry). New plug-ins or new versions can be added by sending a [pull request](https://help.github.com/articles/about-pull-requests/) that includes a single new plug-in entry in JavaScript Object Notation \(JSON\) format.

**Note:** As for all other contributions to the project, pull requests to the registry must be signed off by passing the `--signoff` option to the git commit command to certify that you have the rights to submit this contribution. For more information on this process, see [signing your work](https://www.dita-ot.org/DCO).

The version entries for each plug-in are stored in a file that is named after the plug-in ID as `<plugin-name>.json`. The file contains an array of entries with a pre-defined structure. You should have one entry for each supported version of the plug-in.

|Key|Mandatory|Description|
|---|---------|-----------|
|`name`|yes|Plug-in name|
|`vers`|yes|Plug-in version in [semantic versioning](https://semver.org) format|
|`deps`|yes|Array of dependency entries. The only mandatory plug-in dependency is `org.dita.base`, which defines the supported DITA-OT platform.|
|`url`|yes|Absolute URL to plug-in distribution file|
|`cksum`|no|SHA-256 hash of the plug-in distribution file|
|`description`|no|Description of the plug-in|
|`keywords`|no|Array of keywords|
|`homepage`|no|Plug-in homepage URL|
|`license`|no|License in [SPDX](https://spdx.org/licenses/) format|

**Tip:** To calculate the SHA-256 checksum for the `cksum` key, use `shasum -a 256 <plugin-file\>` on macOS or Linux. With Windows PowerShell, use `[Get-FileHash](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-filehash?view=powershell-6) <plugin-file\> | Format-List`.

|Key|Mandatory|Description|
|---|---------|-----------|
|`name`|yes|Plug-in name|
|`req`|yes|Required plug-in version in [semantic versioning](https://semver.org) format that may contain [ranges](https://docs.npmjs.com/misc/semver#ranges).|

**Note:** Version numbers in the `vers` and `req` keys use the three-digit format specified by [semantic versioning](https://semver.org). An initial development release of a plug-in might start at version 0.1.0, and an initial production release at 1.0.0. If your plug-in requires DITA-OT 3.1 or later, set the `req` key to `>=3.1.0`. Using the greater-than sign allows your plug-in to work with compatible maintenance releases, such as 3.1.3. If the requirement is set to `=3.1.0`, the registry will only offer it for installation on that exact version.

## Sample plug-in entry file

The example below shows an entry for the `DocBook` plug-in. The complete file is available in the registry as [org.dita.docbook.json](https://github.com/dita-ot/registry/blob/master/org.dita.docbook.json).

```language-json
[
  {
    "name": "org.dita.docbook",
    "description": "Convert DITA to DocBook.",
    "keywords": ["DocBook"],
    "homepage": "https://github.com/dita-ot/org.dita.docbook/",
    "vers": "2.3.0",
    "license": "Apache-2.0",
    "deps": [
      {
        "name": "org.dita.base",
        "req": ">=2.3.0"
      }
    ],
    "url": "https://github.com/dita-ot/org.dita.docbook/archive/2.3.zip",
    "cksum": "eaf06b0dca8d942bd4152615e39ee8cfb73a624b96d70e10ab269ed6f8a13e21"
  }
]
```

## Maintaining multiple plug-in versions

When you have multiple versions of a plug-in, include an entry for each version, separated by a comma:

```language-json
[
  {
    "name": "org.example.myplugin",
     ⋮
    "vers": "1.0.1",
     ⋮
  }**,**
  {
    "name": "org.example.myplugin",
     ⋮
    "vers": "2.1.0",
     ⋮
  }
]
```

**Tip:** To publish a new version of your plug-in to the registry, add a new entry to the array in the existing plug-in entry file rather than overwriting an existing entry. This allows users to install the previous version of the plug-in if they are using an older version of DITA-OT.

## Adding custom registries

In addition to the main plug-in registry at [dita-ot.org/plugins](https://www.dita-ot.org/plugins), you can create a registry of your own to store the custom plug-ins for your company or organization.

A registry is just a directory that contains JSON files like the one above; each JSON file represents one entry in the registry. To add a custom registry location, edit the config/configuration.properties file in the DITA-OT installation directory and add the URL for your custom registry directory to the `registry` key value, separating each entry with a space.

**Tip:** Custom registry entries are a simple way to test your own plug-in entry file before submitting to a common registry.

## Testing with a custom registry

To test your plug-in entry with a custom registry:

1.  Fork the plug-in registry, which creates a new repository under your GitHub username — for example, `https://github.com/USERNAME/registry.git`.
2.  Create a new branch for your plug-in entry, and add the JSON file to the branch — for example, create org.example.newPlugin.json in the branch `addPlugin`.
3.  As long as your repository is accessible, that branch now represents a working “custom registry” that can be added to the config/configuration.properties file. Edit the `registry` key and add the raw GitHub URL for the branch that contains the JSON file. With the example username and branch name above, you can add your registry with:

    ```language-properties
    registry=https://raw.githubusercontent.com/USERNAME/registry/addPlugin/ http://plugins.dita-ot.org/
    ```

4.  You can now test the plug-in installation with:

    ```
    dita --install=org.example.newPlugin
    ```

5.  Once you’ve confirmed that the entry works, you can submit a pull request to have your entry added to the common registry.

**Related information**  


[Installing plug-ins](../topics/plugins-installing.md)

[The Art of doing nothing](https://www.oxygenxml.com/events/2019/dita-ot_day.html#the_art_of_doing_nothing)

[All the cool kids are using the Cloud](https://www.oxygenxml.com/events/2019/dita-ot_day.html#all_the_cool_kids_are_using_the_cloud)

[All the cool kids are using JavaScript](https://www.oxygenxml.com/events/2019/dita-ot_day.html#all_the_cool_kids_are_using_javascript)

[AH-WML DITA-to-Word Plug-in](https://www.oxygenxml.com/events/2019/dita-ot_day.html#ah_wml_dita_to_word_plug-in)

[Validation meets publication - Apply your style guide rules during the publication](https://www.oxygenxml.com/events/2018/dita-ot_day.html#apply_your_style_guide_rules_during_the_publication)

[Overview of dita-semia open-source plugins for DITA-OT](https://www.oxygenxml.com/events/2018/dita-ot_day.html#overview_of_dita-semia_open-source_plugins_for_DITA-OT)

[Unit Testing DITA-OT Plugin Extensions](https://www.oxygenxml.com/events/2018/dita-ot_day.html#unit_testing_DITA-OT_plugin_extensions)

[Plug-in installation made easier](https://www.oxygenxml.com/events/2018/dita-ot_day.html#plug-in_installation_made_easier)

[DITA terminology management and checking](https://www.oxygenxml.com/events/2016/dita-ot_day.html#DITA_terminology_management_checking)

