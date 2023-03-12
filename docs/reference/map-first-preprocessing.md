# Map-first preprocessing

DITA-OT 3.0 provides a map-first preprocessing option as an alternative to the default `preprocess` operation. The method, which was introduced in DITA-OT 2.5 as an experimental feature, has been improved and is ready for use in many production scenarios. Map-first-preprocessing provides the same functionality as the default `preprocess`, but takes a different approach.

Whereas the default preprocessing routine handles both maps and topics at the same time, often switching back and forth between map operations and topic operations, the map-first approach only begins processing topics after nearly all map processing is complete. This simplifies the processing logic and creates cleaner module responsibilities, which makes it easier to process only those topics that are actually referenced after filtering, for example, or to only process the map to validate the map structure.

The current preprocessing architecture was established during the DITA 1.0 era when there were fewer DITA features that operated on the map level. Initially, the difference between processing modes was not that great. DITA 1.2 and 1.3 introduced many more map-level features, such as keys and key scopes, that make it difficult to reliably work with topics before all map features have been resolved.

The original preprocessing operation already handles many map operations first, but this was not the original design and requires regular refactoring to handle edge cases. The new map-first preprocessing is designed with this model in mind, improving the overall processing flow and making it more formal about the map-first model. The new model also takes advantage of hashed topic file names in the temporary directory, which simplifies many processing steps, and is better able to handle topics referenced outside of the map directory \(that case has resulted in a variety of issues with the original model\).

**Note:** The map-first preprocessing option is enabled by default in DITA-OT 3.0 for PDF and HTML Help. These formats were chosen because they generate a compiled result file, so temporarily hashed file names should all be invisible to the build. After further testing and feedback, the new option will most likely become the default for other output formats in future versions. Because the DITA-OT development team cannot have access to all varieties of DITA, all edge cases, or even all the ways DITA-OT itself is extended, the switch to default map-first preprocessing for other output formats will be smoother for everyone if more people can test and provide feedback.

## How to use map-first preprocessing

To use \(or test\) map-first preprocessing, call the `preprocess2` Ant target in your custom transformation types instead of using the default `preprocess` target.

For example, if you have a custom HTML5 transformation type named "myhtml", then you may have a plug-in extension that looks this:

```language-xml
<!-- Simple variant: set properties and call default HTML5 -->
<target name="dita2myhtml" depends="myhtml.init,dita2html5"/>

```

This type of extension is quite common, and is used to set default properties for your environment followed by a normal build to use those properties. In this case, you'll need to replace `dita2html5` with the normal HTML5 steps, swapping out `preprocess` for `preprocess2`:

```
<!-- Simple variant: set properties and call default HTML5 -->
<target name="dita2myhtml" 
        depends="myhtml.init,
                 html5.init,
                 build-init,
                 **preprocess2,**
                 html5.topic,
                 html5.map,
                 html5.css"/>
```

**Note:** If you use this simple method for customized PDF or HTML Help builds, you will automatically be using `preprocess2`.

Some custom transformation types already require you to repeat the default dependencies, in which case you should already call `preprocess` directly, as in the following:

```
<!-- More complex variant: add processing steps to default HTML5 -->
<target name="dita2myhtml"
        depends="myhtml.init,
                 build-init,
                 preprocess,
                 local-extensions-after-preprocess,
                 html5.topic,
                 html5.map,
                 html5.css"/>
```

In such cases, the modification is much easier – simply add a `2` to the existing `preprocess` target.

## How to test in a production environment

In some cases, you may be responsible for maintaining transformation types that are actually run by many people on your team or around a company. In this case, you likely need to maintain your existing transformation types based on the backwards-compatible `preprocess` modules, but also want to provide your colleagues with a way to test their own documents using `preprocess2`.

There are several ways to do this. One fairly straightforward approach would be to create a new custom transformation type that is exactly the same, except for preprocessing. For example, if you have a local HTML variant called `myhtml` as above, instead of modifying that transformation directly, you could create a second transformation type called `myhtml-beta` that provides exactly the same support, but with the new map-first preprocessing:

```
*&lt;!-- Original "myhtml" is not modified, used for production --&gt;*
<target name="dita2myhtml5" depends="myhtml.init,dita2html5"/>

*&lt;!-- "myhtml-beta" used to test and provide feedback on preprocess2 --&gt;*
<target name="dita2myhtml-beta" 
        depends="myhtml.init,
                 html5.init,
                 build-init,
                 **preprocess2,**
                 html5.topic,
                 html5.map,
                 html5.css"/>
```

## Known limitations

The `preprocess2` implementation details are subject to change; dependencies within `preprocess2` may be renamed or removed based on feedback.

The internal extension points that run before or after individual steps in the original `preprocess` pipeline \(`preprocess.*.pre/preprocess.*.post`\) are not available in the newer map-first preprocessing pipeline \(`preprocess2`\), which is used in the PDF and HTML Help transformations as of DITA-OT 3.0.

**Related information**  


[We shall call it preprocess2](https://www.oxygenxml.com/events/2017/dita-ot_day.html#preprocess_2)

