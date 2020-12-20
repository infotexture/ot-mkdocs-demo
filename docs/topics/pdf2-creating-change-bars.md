# Generating revision bars

You can generate revision bars in your PDF output by using the `@changebar` and `@color` attributes of the DITAVAL `revprop` element.

The DITA [specification](http://docs.oasis-open.org/dita/dita/v1.3/errata02/os/complete/part3-all-inclusive/langRef/ditaval/ditaval-revprop.html#ditaval-revprop) for the `@changebar` attribute of the `revprop` element simply says:

-   > **`@changebar`**

    > When flag has been set, specify a changebar color, style, or character, according to the changebar support of the target output format. If flag has not been set, this attribute is ignored.


The current version of DITA Open Toolkit uses two `revprop` attribute values to define revision bars:

-   The `@changebar` attribute value defines the style to use for the line. The list of possible values is the same as for other XSL-FO rules \(see [@change-bar-style](http://www.w3.org/TR/xsl/#change-bar-style)\). The default value is groove.

-   The `@color` attribute value specifies the change bar color using any color value recognized by XSL-FO, including the usual color names or a hex color value. The default value is black.


```language-xml
<revprop action="flag" changebar="solid" color="green"/>
```

DITA-OT uses a default offset of 2 mm to place the revision bar near the edge of the text column. The offset, placement and width are not currently configurable via attribute values.

XSL-FO 1.1 does not provide for revision bars that are not rules, so there is no way to get text revision indicators instead of rules, for example, using a number in place of a rule. Antenna House Formatter provides a proprietary extension to enable this, but the DITA-OT PDF transformation does not take advantage of it.

