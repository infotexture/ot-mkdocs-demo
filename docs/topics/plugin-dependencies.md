# Plug-in dependencies

A DITA-OT plug-in can be dependent on other plug-ins. Prerequisite plug-ins are installed first, which ensures that DITA-OT handles XSLT overrides correctly.

The `<require>` element in the `plugin.xml` file specifies whether the plug-in has dependencies. Use `<require>` elements to specify prerequisite plug-ins, in order from most general to most specific.

If a prerequisite plug-in is missing, DITA-OT prints a warning during installation. To suppress the warning but keep the installation order if both plug-ins are present, add `importance="optional"` to the `<require>` element.

If a plug-in can depend on any one of several optional plug-ins, separate the plug-in IDs with a vertical bar. This is most useful when combined with `importance="optional"`.

## Example: Plug-in with a prerequisite plug-in

The following plug-in will only be installed if the plug-in with the ID `com.example.primary` is available. If that plug-in is not available, a warning is generated and the installation operation fails.

```
<plugin id="com.example.builds-on-primary">
  <!-- ... Extensions here -->
  <require plugin="com.example.primary"/>
</plugin>
```

## Example: Plug-in that has optional plug-ins

The following plug-in will only be installed if either the plug-in with the ID `pluginA` or the plug-in with the ID `pluginB` is available. If neither of those plug-ins are installed, a warning is generated but the installation operation is completed.

```
<plugin id="pluginC">
  <!-- ...extensions here -->
  <require plugin="pluginA|pluginB" importance="optional"/>
</plugin>
```

**Related information**  


[Plug-in coding conventions](../topics/plugin-coding-conventions.md)

