# Adding custom headers and footers

You add a custom header to include a publication title, company logo, or other common branding elements in HTML output. A custom footer can also be added with copyright information, legal boilerplate, or other fine print.

In HTML5 output, the contents of the header file will be wrapped in an HTML5 `header` element with the `@role` attribute set to banner. The footer file contents are wrapped in an HTML5 `footer` element with the `@role` attribute set to contentinfo.

For example, the DITA-OT documentation includes a simple header banner with the publication title and a horizontal rule to separate the header from the generated topic content:

```
<div class="header">
  <p>DITA Open Toolkit</p>
  <hr/>
</div>
```

**Note:** Header and footer files should be specified using absolute paths and must contain valid XML. A common practice is to place all content into a `div` element.

1.  Set args.hdr to include an XML file as a running header that appears above the page content.

2.  Set args.ftr to include an XML file as a running footer that appears below the page content.

3.  Add custom CSS rules to style headers and/or footers.

    For example, the DITA-OT documentation stylesheet includes the following header rules:

    ```
    .header {
      margin-bottom: 1rem;
      padding: 0 12px;
    }
    
    .header p {
      color: var(--headings-color);
      font-size: 1.5rem;
      margin: 0 0 16px;
    }
    
    .header hr {
      border: 0;
      border-bottom: 1px solid var(--secondary-light);
      height: 0;
    }
    ```


**Tip:** For an example of HTML output generated using this method, see the HTML5 version of the DITA-OT documentation included in the installation folder under doc/index.html.

