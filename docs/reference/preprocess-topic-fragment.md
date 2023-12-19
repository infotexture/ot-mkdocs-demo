# Resolve topic fragments and code references \(`topic-fragment`\)

The `topic-fragment` step expands content references to elements in the same topic and resolves references made with the `<coderef>` element. This step is implemented in SAX pipes.

Content references to elements in the same topic are defined via same-topic fragments such as `#./ID` in URIs.

The `<coderef>` element is used to reference code stored externally in non-XML documents. During the pre-processing step, the referenced content is pulled into the containing `<codeblock>` element.

**Related information**  


[Extended codeblock processing](../reference/extended-functionality.md)

