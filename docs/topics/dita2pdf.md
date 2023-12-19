# PDF

The pdf transformation generates output in Portable Document Format.

This transformation was originally created as a plug-in and maintained outside of the main toolkit code. It was created as a more robust alternative to the demo PDF transformation in the original toolkit, and thus was known as PDF2. The plug-in was bundled into the default toolkit distribution with release 1.4.3.

To run the PDF transformation, set the **transtype** parameter to pdf, or pass the **--format**=pdf option to the `dita` command line.

```
``dita`` **--input**=*input-file* **--format**=pdf
```

where:

-   *input-file* is the DITA map or DITA file that you want to process.

**Related information**  


[Common parameters](../parameters/parameters-base.md)

[PDF parameters](../parameters/parameters-pdf.md)

[Generating revision bars](../topics/pdf2-creating-change-bars.md)

