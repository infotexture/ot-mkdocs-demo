# Implementation-dependent features

For certain features, the DITA specification allows conforming processors to choose between different implementation alternatives. In these cases, there may be differences in behavior when DITA content is handled by different processors. DITA-OT supports implementation-specific features by applying one or more of the permissible processing approaches.

## Chunking

DITA content can be divided or merged into new output documents in different ways, depending on the value of the `@chunk` attribute.

DITA-OT supports the following chunking methods:

-   select-topic
-   select-document
-   select-branch
-   by-topic
-   by-document
-   to-content
-   to-navigation.

When no chunk attribute values are given, no chunking is performed.

**Note:** For HTML-based transformation types, this is effectively equivalent to select-document and by-document defaults.

Error recovery:

-   When two tokens from the same category are used, no error or warning is thrown.
-   When an unrecognized chunking method is used, no error or warning is thrown.

## Filtering

Error recovery:

-   When there are multiple `revprop` elements with the same `@val` attribute, no error or warning is thrown
-   When multiple prop elements define a duplicate attribute and value combination, attribute default, or fall-back behavior, the DOTJ007W warning is thrown.

## Debugging attributes

The debug attributes are populated as follows:

-   **xtrf**

    The XML trace filename is used to store the absolute system path of the original source document.

-   **xtrc**

    The XML trace counter stores an element counter with the following format:

    ```
    element-name ":" integer-counter ";" line-number ":" column-number
    ```


## Image scaling

If both height and width attributes are given, the image is scaled non-uniformly.

If the scale attribute is not an unsigned integer, no error or warning is thrown during preprocessing.

## Map processing

When a `topicref` element that references a map contains child `topicref` elements, the DOTX068W error is thrown and the child `topicref` elements are ignored.

## Link processing

When the value of a hyperlink reference in the `@href` attribute is not a valid URI reference, the DOTJ054E error is thrown. Depending on the [processing-mode](../parameters/parameters-base.md#processing-mode) setting, error recovery may be attempted.

## Copy-to processing

When the `@copy-to` attribute is specified on a `topicref`, the content of the `shortdesc` element is not used to override the short description of the topic.

## Coderef processing

When `coderef` elements are used within code blocks to reference external files with literal code samples, the system default character set is used as the target file encoding unless a different character set is explicitly defined via the mechanisms described under [Character set definition](extended-functionality.md#coderef-charset).

