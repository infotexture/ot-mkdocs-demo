# Generate lists \(`gen-list`\)

The `gen-list` step examines the input files and creates lists of topics, images, document properties, or other content. These lists are used by later steps in the pipeline. This step is implemented in Java.

For example, one list includes all topics that make use of the conref attribute; only those files are processed during the conref stage of the build. The list file name name is derived from the list file property. For example, the `conref.list` file is generated for “conreffile” and a corresponding list property is provided for each generated list, in this case “conreflist”.

The result of this step is a set of several list files in the temporary directory, including dita.list and dita.xml.properties.

|List file property|List file|Usage|
|------------------|---------|-----|
|canditopicsfile|`canditopics.list`| |
|conreffile|`conref.list`|Documents that contain conref attributes that need to be resolved in preprocess.|
|conreftargetsfile|`conreftargets.list`| |
|copytosourcefile|`copytosource.list`| |
|flagimagefile|`flagimage.list`| |
|fullditamapandtopicfile|`fullditamapandtopic.list`|All of the ditamap and topic files that are referenced during the transformation. These may be referenced by href or conref attributes.|
|fullditamapfile|`fullditamap.list`|All of the ditamap files in dita.list|
|fullditatopicfile|`fullditatopic.list`|All of the topic files in dita.list|
|hrefditatopicfile|`hrefditatopic.list`|All of the topic files that are referenced with an href attribute|
|hreftargetsfile|`hreftargets.list`|Link targets|
|htmlfile|`html.list`|Resource files|
|imagefile|`image.list`|Image files that are referenced in the content|
|outditafilesfile|`outditafiles.list`| |
|resourceonlyfile|`resourceonly.list`| |
|subjectschemefile|`subjectscheme.list`| |
|subtargetsfile|`subtargets.list`| |
|tempdirToinputmapdir.relative.value| | |
|uplevels| | |
|user.input.dir| |Absolute input directory path|
|user.input.file.listfile| |Input file list file|
|user.input.file| |Input file path, relative to the input directory|

