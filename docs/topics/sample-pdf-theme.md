# Sample theme file

Theme files can be written in either [JSON](https://json.org) or [YAML](https://yaml.org) format. The docsrc/samples/themes folder in the DITA-OT installation directory provides several examples.

**Note:** The examples provided here are all in YAML format, which is generally more compact and readable than JSON.

The YAML theme file used to produce the PDF output for the DITA-OT documentation is included in the installation directory as dita-ot-dir/docsrc/samples/themes/dita-ot-docs-theme.yaml.

The examples below include excerpts from this theme that show common customizations. You can adapt these examples for your own requirements.

**Tip:** For an overview of the elements and other settings that the theme plug-in supports, see [Styles](../resources/theme/Styles.md), [Page settings](../resources/theme/Page-settings.md), [Header and footer](../resources/theme/Header-and-footer.md), and [Variables](../resources/theme/Variables.md).

## Setting custom colors

Like in CSS or [Sass](http://sass-lang.com), you can use [Variables](../resources/theme/Variables.md) to define brand colors and other shared values, and re-use these them in other [Styles](../resources/theme/Styles.md) using semantic references such as `$brand-color-primary`.

```
brand:
  color:
    primary: '#1d365d'
    secondary: '#6c757d'
    tertiary: '#bac8d1'
    inverse: '#e9ecef'
    links: '#3563ab'
    note:
      background:
        attention: '#fff3cd'
        caution: '#f8d7da'
        info: '#dce4f0'
        tip: '#d1e7dd'
```

## Defining custom font stacks

You can also use [Variables](../resources/theme/Variables.md) to specify a prioritized list of one or more font family names and reference these values in the `font-family` property of other [style](../resources/theme/Styles.md) keys.

```
pdf2:
  font:
    sans: 'Helvetica, Arial Unicode MS, Tahoma, Batang, SimSun'
    serif: 'Times New Roman, Times, Arial Unicode MS, Tahoma, Batang, SimSun'
    monospaced: 'Courier New, Courier, Arial Unicode MS, Tahoma, Batang, SimSun'
```

This theme uses the default font stacks from the default `org.dita.pdf2` plug-in, but the same approach can be used to define other font families as required by your corporate identity.

The font variables defined here under the `pdf2` prefix could just as well be added to the `brand` key, or under a company name prefix and re-used elsewhere with references such as `$company-font-sans`.

## Defining page sizes

[Page settings](../resources/theme/Page-settings.md) include page `size`, `orientation`, and margins.

```
page:
  size: PA4
  mirror-margins: true
```

The DITA-OT documentation theme uses the `PA4` page size, a 21 × 28 cm transitional format suitable for printing on both A4 and US Letter paper.

The `mirror-margins` key sets up facing pages for double-sided documents, so the margins of the left page are a mirror image of those on the right.

## Extending and overriding themes

You can [extend](../resources/theme/Extending-themes.md) one theme with another. The samples in the DITA-OT installation directory include additional theme files that can be used to override the `PA4` page size in the documentation theme with either A4 or Letter.

```
# Sample PDF theme that changes page size for printing on A4 paper
extends: ./dita-ot-docs-theme.yaml
page:
  size: A4
```

```
# Sample PDF theme that changes page size for printing on US Letter paper
extends: ./dita-ot-docs-theme.yaml
page:
  size: Letter
```

When one of these theme extensions is passed to the dita command via the --theme option, the `page-size` value in the extending theme takes precedence over the original value in dita-ot-docs-theme.yaml.

If you add any new keys to a theme extension, they will be overlaid onto the keys from the extended theme.

## Setting up headers and footers

The documentation theme includes sample customizations to adjust the content of the running headers and footers that appear on each page.

```
header:
  color: $brand-color-secondary
  display-align: before
  end-indent: 10mm
  font-family: $pdf2-font-sans
  padding-after: 6pt
  padding-before: 12pt
  start-indent: 10mm
  odd:
    content: '{chapter}'
    text-align: end
  even:
    content: '{title}'
    text-align: start
```

These settings use the secondary brand color for page headers \(as defined above under [Setting custom colors](sample-pdf-theme.md#colors)\), the sans-serif font families defined above under [Defining custom font stacks](sample-pdf-theme.md#fonts), and position the content with indentation and padding.

```
footer:
  color: $brand-color-secondary
  end-indent: 10mm
  font-family: $pdf2-font-sans
  padding-after: 12pt
  padding-before: 6pt
  start-indent: 10mm
  odd:
    content: '{folio}'
    font-weight: bold
    text-align: end
  even:
    content: '{folio}'
    font-weight: bold
    text-align: start
```

These settings use the `{folio}` field to place the current page number on the outside edges of each page footer. The `content` key may include combinations of static text, or reference variables using curly braces. For details on the available options, see [Header and footer](../resources/theme/Header-and-footer.md) and [Variables](../resources/theme/Variables.md).

## Adding an image to the cover page

The `cover` and `cover-title` [Styles](../resources/theme/Styles.md) can be used to add a background image and adjust the formatting and placement of the document title.

```
cover:
  background-image: dita-ot-logo-inverse.svg
  background-repeat: no-repeat
  height: 25.7cm
cover-title:
  color: $brand-color-primary
  font-size: 36pt
  font-weight: bold
  line-height: 1.5
  space-before: 195mm
```

The DITA-OT documentation theme references a background image stored in the same folder as the theme file, and places the title at the bottom of the page by setting the `space-before` property for the `cover-title`.

**Tip:** The latest version of the documentation theme is available on GitHub: [dita-ot-docs-theme.yaml](https://github.com/dita-ot/docs/blob/develop/samples/themes/dita-ot-docs-theme.yaml).

