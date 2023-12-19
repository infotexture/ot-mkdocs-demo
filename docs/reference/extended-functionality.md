# Extended codeblock processing

DITA-OT provides additional processing support beyond that which is mandated by the DITA specification. These extensions can be used to define character encodings or line ranges for code references, normalize indendation, add line numbers or display whitespace characters in code blocks.

## Character set definition

For `<coderef>` elements, DITA-OT supports defining the code reference target file encoding using the `@format` attribute. The supported format is:

```
format (";" space* "charset=" charset)?
```

If a character set is not defined, the system default character set will be used. If the character set is not recognized or supported, the DOTJ052E error is thrown and the system default character set is used as a fallback.

```language-xml
<coderef href="unicode.txt" format="txt; charset=UTF-8"/>
```

As of DITA-OT 3.3, the default character set for code references can be changed by adding the **default.coderef-charset** key to the [configuration.properties](../parameters/configuration-properties-file.md) file:

```language-properties
default.coderef-charset = ISO-8859-1
```

The character set values are those supported by the Java [Charset](https://docs.oracle.com/javase/8/docs/api/java/nio/charset/Charset.html) class.

**Note:** As of DITA-OT 4.0, the default character set for code references has been changed from the system default encoding to UTF-8.

## Line range extraction

Code references can be limited to extract only a specified line range by defining the `line-range` pointer in the URI fragment. The format is:

```
uri ("#line-range(" start ("," end)? ")" )?
```

Start and end line numbers start from 1 and are inclusive. If the end range is omitted, the range ends on the last line of the file.

```language-xml
<coderef href="Parser.scala#line-range(5,10)" format="scala"/>
```

Only lines from 5 to 10 will be included in the output.

## RFC 5147

DITA-OT also supports the line position and range syntax from [RFC 5147](http://tools.ietf.org/html/rfc5147). The format for line range is:

```
uri ("#line=" start? "," end? )?
```

Start and end line numbers start from 0 and are inclusive and exclusive, respectively. If the start range is omitted, the range starts from the first line; if the end range is omitted, the range ends on the last line of the file. The format for line position is:

```
uri ("#line=" position )?
```

The position line number starts from 0.

```language-xml
<coderef href="Parser.scala#line=4,10" format="scala"/>
```

Only lines from 5 to 10 will be included in the output.

## Line range by content

Instead of specifying line numbers, you can also select lines to include in the code reference by specifying keywords \(or “tokens”\) that appear in the referenced file.

DITA-OT supports the `token` pointer in the URI fragment to extract a line range based on the file content. The format for referencing a range of lines by content is:

```
uri ("#token=" start? ("," end)? )?
```

Lines identified using start and end tokens are exclusive: the lines that contain the start token and end token will be not be included. If the start token is omitted, the range starts from the first line in the file; if the end token is omitted, the range ends on the last line of the file.

Given a Haskell source file named `fact.hs` with the following content,

```
-- START-FACT
fact :: Int -> Int
fact 0 = 1
fact n = n * fact (n-1)
-- END-FACT
main = print $ fact 7
```

a range of lines can be referenced as:

```language-xml
<coderef href="fact.hs#token=START-FACT,END-FACT"/>
```

to include the range of lines that follows the `START-FACT` token on Line 1, up to \(but not including\) the line that contains the `END-FACT` token \(Line 5\). The resulting `<codeblock>` would contain lines 2–4:

```language-haskell
fact :: Int -> Int
fact 0 = 1
fact n = n * fact (n-1)
```

**Tip:** This approach can be used to reference code samples that are frequently edited. In these cases, referencing line ranges by line number can be error-prone, as the target line range for the reference may shift if preceding lines are added or removed. Specifying ranges by line content makes references more robust, as long as the `token` keywords are preserved when the referenced resource is modified.

## Whitespace normalization

DITA-OT can adjust the leading whitespace in code blocks to remove excess indentation and keep lines short. Given an XML snippet in a codeblock with lines that all begin with spaces \(indicated here as dots “·”\),

```language-xml
··<subjectdef keys="audience">
····<subjectdef keys="novice"/>
····<subjectdef keys="expert"/>
··</subjectdef>
```

DITA-OT can remove the leading whitespace that is common to all lines in the code block. To trim the excess space, set the `@outputclass` attribute on the `<codeblock>` element to include the `normalize-space` keyword.

In this case, two spaces \(“··”\) would be removed from the beginning of each line, shifting content to the left by two characters, while preserving the indentation of lines that contain additional whitespace \(beyond the common indent\):

```language-xml
<subjectdef keys="audience">
··<subjectdef keys="novice"/>
··<subjectdef keys="expert"/>
</subjectdef>
```

## Whitespace visualization \(PDF\)

DITA-OT can be set to display the whitespace characters in code blocks to visualize indentation in PDF output.

To enable this feature, set the `@outputclass` attribute on the `<codeblock>` element to include the `show-whitespace` keyword.

When PDF output is generated, space characters in the code will be replaced with a middle dot or “interpunct” character \( `·` \); tab characters are replaced with a rightwards arrow and three spaces \( `→   ` \).

```
	for i in 0..10 {
		println(i)
	}
```

## Line numbering \(PDF\)

DITA-OT can be set to add line numbers to code blocks to make it easier to distinguish specific lines.

To enable this feature, set the `@outputclass` attribute on the `<codeblock>` element to include the `show-line-numbers` keyword.

```
	for i in 0..10 {
		println(i)
	}
```

**Related information**  


[Resolve topic fragments and code references \(topic-fragment\)](../reference/preprocess-topic-fragment.md)

