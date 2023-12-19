# Extension point reference

DITA Open Toolkit provides a series of extension points that can be used to integrate changes into the core code. Extension points are defined in the `plugin.xml` file for each plug-in. When plug-ins are installed, DITA-OT makes each extension visible to the rest of the toolkit.

Depending on which extension points you use, your custom code will either run whenever output is generated, before or after certain processing stages, or only with certain transformation types.

## Extension points govern when code runs

-   To run a custom Ant target after the pre-processing stage regardless of transformation type, use **depend.preprocess.post**
-   To run an Ant target before the `copy-html` step when generating HTML output, use **depend.preprocess.copy-html.pre**

## Checking the transformation type

If you want to isolate your custom code so it only runs when output is generated for a particular transformation type, you can define a condition that checks the transtype before running the custom code.

```
<!-- Add a condition that checks the transtype -->
<condition property="isYourTranstype">
  <matches pattern="your.transtype" string="${transtype}"/>
</condition>
```

You can then check this condition before running your custom code:

```
<!-- Check the condition before running your target -->
<target name="your-target" if="${isYourTranstype}">
  ⋮
</target>
```

**Related information**  


[Extending the DITA Open Toolkit: How crazy can you get?](https://www.oxygenxml.com/events/2014/dita-ot_day.html#Extending_the_DITA_Open_Toolkit)

