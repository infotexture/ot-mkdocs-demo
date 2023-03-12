# Books

Several DITA-related publications include information on configuring and customizing DITA Open Toolkit with detailed examples on creating custom plug-ins for PDF output.

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


[Customizing PDF output](../topics/pdf-customization.md)

