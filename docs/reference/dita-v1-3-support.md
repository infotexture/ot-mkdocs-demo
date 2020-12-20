# DITA 1.3 support

DITA Open Toolkit 3.6 provides processing support for the OASIS DITA 1.3 specification. Initial preview support for this specification was added in version 2.0 of the toolkit; version 2.2 extended this foundation to support key scopes and branch filtering along with additional DITA 1.3 features.

Because DITA 1.3 is fully backwards compatible with previous DITA DTDs and schemas, DITA-OT provides the 1.3 materials as the default grammar files for processing. The XML Catalog resolution maps any references for unversioned DITA document types to the 1.3 versions. All processing ordinarily dependent on the 1.0, 1.1, or 1.2 definitions continues to work as usual, and any documents that make use of the newer DITA 1.3 elements or attributes will be supported with specific new processing.

## Major features of DITA 1.3

The following DITA 1.3 features are supported in DITA Open Toolkit.

-   [Scoped keys](http://docs.oasis-open.org/dita/dita/v1.3/errata01/os/complete/part1-base/archSpec/base/keyScopes.html) supported using DITA 1.3 `@keyscope` attribute
-   [Branch filtering](http://docs.oasis-open.org/dita/dita/v1.3/errata01/os/complete/part1-base/archSpec/base/branch-filtering.html) using `ditavalref` elements in a map
-   Support formatting based on new XML Mention elements, such as adding angle brackets around elements tagged with `xmlelement` and adding `@` before attributes tagged with `xmlatt`
-   New highlighting elements `line-through` and `overline`
-   Support for profiling based on `@deliveryTarget` attribute
-   Support for the new `@orient` attribute for rotating tables
-   Profile \(filter or flag\) based on [groups within profiling attributes](http://docs.oasis-open.org/dita/dita/v1.3/errata01/os/complete/part1-base/archSpec/base/usage-of-conditional-processing-attributes.html)
-   `@keyref` and related key referencing attributes supported on `object`
-   New in-topic link syntax using `.` in place of the topic ID: `#./figure`
-   Support for additional new elements, such as the `div` element for grouping
-   Support `@cascade` attribute in maps \(processing defaults to the value `merge`, which is the [default cascade operation](http://docs.oasis-open.org/dita/dita/v1.3/errata01/os/complete/part1-base/archSpec/base/example-how-cascade-att-functions.html) described by the DITA specification\)

**Note:** For the latest status information on DITA 1.3-related features and fixes, see the [DITA 1.3 label](https://github.com/dita-ot/dita-ot/issues?q=label%3A%22DITA+1.3%22) in the GitHub issues tracker.

**Related information**  


[Accessibility in DITA-OT](https://www.oxygenxml.com/events/2017/dita-ot_day.html#Accessibility_DITA-OT)

[RNG to DTD and XSD using the DITA Open Toolkit](https://www.oxygenxml.com/events/2014/dita-ot_day.html#RNG_to_DTD_and_XSD_using_the_DITA_Open_Toolkit)

[DITA 1.3 Part 3 latest errata version: All-Inclusive Edition \(HTML\)](http://docs.oasis-open.org/dita/dita/v1.3/dita-v1.3-part3-all-inclusive.html)

[DITA 1.3 Part 3 latest errata version: All-Inclusive Edition \(PDF\)](http://docs.oasis-open.org/dita/dita/v1.3/dita-v1.3-part3-all-inclusive.pdf)

[DITA Version 1.3 Errata 01 \(Distribution ZIP of the DITA source\)](http://docs.oasis-open.org/dita/dita/v1.3/errata01/os/complete/part3-all-inclusive/dita-v1.3-errata01-os-part3-all-inclusive-complete-dita.zip)

[OASIS DITA Technical Committee](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=dita)

[OASIS DITA Adoption Technical Committee](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=dita-adoption)

