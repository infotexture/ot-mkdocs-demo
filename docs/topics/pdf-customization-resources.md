# Resources for custom PDF plug-ins

There are several external resources that can help you generate and refine custom PDF plug-ins for DITA Open Toolkit.

## PDF Plugin Generator

This online tool, developed and maintained by Jarno Elovirta, enables you to generate a PDF customization plug-in automatically.

The application at [dita-generator.elovirta.com](http://dita-generator.elovirta.com/) walks you through the process of creating a custom PDF plug-in and allows you to adjust a variety of settings for your PDF output. For example, you can:

-   Define the target environment by selecting a version of DITA-OT
-   Select the XSL formatting engine \(FOP, Antenna House Formatter, or RenderX XEP\)
-   Specify page size, columns, and margins
-   Select from \(limited\) options for headers and footers
-   Specify layout options for chapters
-   Select formatting for the following publication components:

    -   Normal text
    -   Headings \(levels one through four\)
    -   Titles for sections and examples
    -   Tables and figures
    -   Notes and examples
    -   Lists \(unordered, ordered, and definition\)
    -   Code blocks and pre-formatted text
    -   Inline elements such as links and trademarks
    For each component, you can specify:

    -   Font family, size, weight, and style
    -   Color and background color
    -   Alignment, indentation, spacing, and padding

**Tip:** The PDF Plugin Generator should be your first stop as you start developing a brand-new PDF customization plug-in.

## **DITA for Print: A DITA Open Toolkit Workbook** \(Second Edition, 2017\)

Authored by Leigh W. White, DITA Specialist at IXIASOFT, and published by XML Press, **DITA for Print** walks readers through developing a PDF customization from scratch.

Here is an excerpt from the back cover:

> **DITA for Print** is for anyone who wants to learn how to create PDFs using the DITA Open Toolkit without learning everything there is to know about XSL-FO, XSLT, or XPath, or even about the DITA Open Toolkit itself. **DITA for Print** is written for non-programmers, by a non-programmer, and although it is written for people who have a good understanding of the DITA standard, you don’t need a technical background to get custom PDFs up and running quickly.

This is an excellent, long-needed resource that was initially developed in 2013 for DITA-OT 1.8.

The second edition has been revised to cover DITA Open Toolkit Version 2, including customizing the DITA 1.3 troubleshooting topic type, localization strings, bookmarks, and the new back-cover functionality.

**Important:**

The first edition of **DITA for Print** recommended copying entire files from the PDF2 plug-in to your custom plug-in. The DITA-OT project — and the second edition of the book — do not recommend this practice.

Instead, you should copy only the specific attribute sets and templates that you want to override. Following this practice will more cleanly isolate your customizations from the DITA-OT code, which will make it easier for you to update your plug-ins to work with future versions of DITA-OT.

## **DITA for Practitioners: Volume 1, Architecture and Technology** \(2012\)

Authored by Eliot Kimber and published by XML Press, this seminal resource contains a chapter dedicated to DITA Open Toolkit: “Running, Configuring, and Customizing the Open Toolkit”. In addition to a robust overview of DITA-OT customization and extension, the chapter contains a detailed example of customizing a PDF plug-in to specify 7" × 10" paper size and custom fonts for body text and headers.

The DITA-OT chapter in **DITA for Practitioners: Volume 1** was written for DITA-OT 1.5.4, which was the latest stable version at the time it was written.

**Related information**  


[Twisted XSLT Tricks: Making Column Switching Work for FOP](https://www.oxygenxml.com/events/2018/dita-ot_day.html#twisted_xslt_tricks)

[DITA Open Toolkit PDF Plugins Without Fuss, Muss, or Writing XSL-FO](https://www.oxygenxml.com/events/2014/dita-ot_day.html#DITA_Open_Toolkit_PDF_plugins_without_fuss_muss_or_writing_XSL-FO)

[PDFs from the DITA Open Toolkit: The Easy and the Not-so-Easy](https://www.oxygenxml.com/events/2014/dita-ot_day.html#PDFs_from_the_DITA_Open_Toolkit)

