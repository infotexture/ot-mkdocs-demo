# PDF themes

DITA-OT 4.0 includes the `com.elovirta.pdf` plug-in, which extends the default PDF2 plug-in with a new theme parameter. The --theme option takes a path to a theme file and changes the styling of the PDF output without requiring changes to XSLT stylesheets.

Themes can be used to adjust basic settings like cover page images, page sizes, numbering, font properties, background colors and borders, spacing, and running content like page headers and footers.

To generate PDF output with a custom theme, pass the theme file to the dita command with the --theme option:

```syntax-bash
dita --project=samples/project-files/pdf.xml \
     --theme=path/to/custom-theme-file.yaml
```

The following topics provide details on the theme file formats and supported configuration options.

**Related information**  


[PDF customization approaches](../topics/pdf-customization-approaches.md)

[Custom PDF plug-ins](../topics/pdf-customization-plugins.md)

[Simpler custom PDFs - The technical details](https://www.oxygenxml.com/events/2022/dita-ot_day.html#Simpler_custom_PDFs_The_technical_details)

[Simpler custom PDFs - The user perspective](https://www.oxygenxml.com/events/2022/dita-ot_day.html#Simpler_custom_PDFs_The_user_perspective)

