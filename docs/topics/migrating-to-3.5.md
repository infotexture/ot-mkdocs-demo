# Migrating to release 3.5

DITA-OT 3.5 includes support for additional input resources, an alternative subcommand syntax for the dita command, and an initial preview of features for the latest draft of the upcoming DITA 2.0 standard.

**Note:** This topic provides a summary of changes in DITA-OT 3.5 that may require modifications to custom stylesheets or plug-ins. For more information on changes in this release, see the [DITA-OT 3.5 Release Notes](https://www.dita-ot.org/3.5/release-notes/).

## New subcommands

The dita command line interface has been refactored to support subcommands for common operations.

**Important:** The new subcommands supersede the deprecated X-Toolkit–style single-hyphen keyword variants \(such as -install\), and the corresponding GNU-style option keywords preceded by two hyphens \(such as --install\).

-   **dita install**

    Installs or reloads plug-ins \(replaces dita --install\)

-   **dita plugins**

    Prints a list of installed plug-ins \(replaces dita --plugins\)

-   **dita transtypes**

    Prints a list of installed transformation types, or *output formats* \(replaces dita --transtypes\)

-   **dita uninstall**

    Removes and deletes a plug-in \(replaces dita --uninstall\)

-   **dita version**

    Prints version information and exits \(replaces dita --version\)


**Tip:** The double-hyphen option syntax has been retained for backwards compatibility, so if you use commands like dita --install in scripts, they will still work, but you may want to migrate your scripts to the new subcommand syntax.

## Legacy constructs removed

DITA-OT 3.5 no longer includes the following legacy properties, list files, and targets, which were deprecated in previous releases. These constructs were no longer used in recent releases, and have now been removed entirely.

The following Ant targets have been removed from the pre-processing pipeline:

-   `mappull` and `mappull-check`, which were used to pull metadata \(such as navtitle\) into the map from referenced topics prior to DITA-OT 2.2 \(merged with `move-meta-entries`\)
-   `conref-check`, deprecated since 2.3
-   `coderef`, which was used to resolve code references in input files prior to 2.3 \(merged with `topic-fragment`\)
-   `copy-subsidiary` and `copy-subsidiary-check`, which were used to copy files to the temporary directory prior to 2.1

Recent DITA-OT versions provide alternative mechanisms to achieve the same results, such as the `ditafileset` element to select resources in the temporary directory.

Along with the obsolete targets, the following Ant properties have been removed:

-   `canditopicsfile`
-   `canditopicslist`
-   `conreffile`
-   `conreflist`
-   `conreftargetsfile`
-   `conreftargetslist`
-   `copytosourcefile`
-   `copytosourcelist`
-   `fullditamapandtopicfile`
-   `fullditamapandtopiclist`
-   `fullditamapfile`
-   `fullditamaplist`
-   `fullditatopicfile`
-   `fullditatopiclist`
-   `hrefditatopicfile`
-   `hrefditatopiclist`
-   `hreftargetsfile`
-   `hreftargetslist`
-   `htmlfile`
-   `htmllist`
-   `imagefile`
-   `imagelist`
-   `outditafilesfile`
-   `outditafileslist`
-   `resourceonlyfile`
-   `resourceonlylist`
-   `subjectschemefile`
-   `subjectschemelist`
-   `subtargetsfile`
-   `subtargetslist`
-   `user.input.file.listfile`
-   `user.input.file`

The following obsolete list files are no longer generated in the temporary directory:

-   canditopics.list
-   conref.list
-   conreftargets.list
-   copytosource.list
-   fullditamap.list
-   fullditamapandtopic.list
-   fullditatopic.list
-   hrefditatopic.list
-   hreftargets.list
-   html.list
-   image.list
-   outditafiles.list
-   resourceonly.list
-   subjectscheme.list
-   subtargets.list
-   user.input.file.list
-   usr.input.file.list

For example, if your plug-in previously used the `fullditatopicfile` to select resources in the temporary directory like this:

```
<xslt basedir="${dita.temp.dir}"
      destdir="${output.dir}"
      includesfile="${dita.temp.dir}${file.separator}${fullditatopicfile}"
      style="${args.xsl}">
  [...]
</xslt>
```

With DITA-OT 2.4 or newer, use the `ditafileset` element instead:

```
<xslt basedir="${dita.temp.dir}"
      destdir="${output.dir}"
      style="${args.xsl}">
  <ditafileset format="dita" processingRole="normal"/>
  [...]
</xslt>
```

If your plug-in previously used the `user.input.file.listfile` to process the start map like this:

```
<xslt [...]
      includesfile="${dita.temp.dir}${file.separator}${user.input.file.listfile}"/>
```

Use the `ditafileset` element as follows:

```
<xslt [...] >
  <ditafileset input="true" format="ditamap"/>
</xslt>
```

## Adjusting output file names

Two new parameters can be used to dynamically adjust the names and locations of output files in transformations that use the map-first pre-processing routine \(`preprocess2`\).

These parameters can be passed on the command line, or included in a custom plug-in via `property` elements in an Ant script as described in [Adjusting file names in map-first pre-processing](plugin-rewrite-rules.md).

-   Use result.rewrite-rule.class to rewrite filenames with a Java class that implements the `org.dita.dost.module.RewriteRule` interface
-   Use result.rewrite-rule.xsl to rewrite via an XSLT stylesheet

