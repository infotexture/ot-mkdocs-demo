# Handling content outside the map directory

By default, DITA-OT assumes content is located in or beneath the directory containing the DITA map file. The **generate.copy.outer** parameter can be used to adjust how output is generated for content that is located outside the map directory.

## Background

This is an issue in the following situations:

-   The DITA map is in a directory that is a peer to directories that contain referenced objects.
-   The DITA map is in a directory that is below the directories that contain the referenced objects.

Let’s assume that the directory structure for the DITA content looks like the following:

```
images/
  fig.png
maps/
  start.ditamap
topics/
  topic.dita
```

The DITA map is in the `maps` directory, the topics are in the `topics` directory, and the images are in the `images` directory.

## Exclude content outside the map directory

Let’s assume that you run the HTML5 transformation. By default, DITA-OT uses the **generate.copy.outer** parameter with a value of 1, which means that no output is generated for content that is located outside the DITA map directory.

You receive only the following output:

```
index.html
commonltr.css
commonrtl.css
```

The `index.html` file contains the navigation structure, but all the links are broken, since no HTML files were built for the topics.

How do you fix this? By adjusting the parameter setting to shift the output directory.

## Shift the output directory to include all content

To preserve the links to referenced topics and images and make it easier to copy the output directory, set the **generate.copy.outer** parameter to 3.

Now your output directory structure resembles the structure of the source directory:

```
images/
  fig.png
maps/
  index.html
topics/
  topic.html
commonltr.css
commonrtl.css
```

The `index.html` file is in the `maps` directory, the HTML files for the topics are in the `topics` directory, and the referenced images are in the `images` directory.

**Tip:** If **args.csspath** is not set, the default CSS files \(and any custom CSS files specified via **args.css**\) will be copied to the root level of the output folder. To copy CSS files to an output subfolder named `css`, set **args.csspath** to css.

