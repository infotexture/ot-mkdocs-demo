# Version and support information

You can use these extension points to define version and support information for a plug-in. Currently, DITA-OT does not do anything with this information, but it might do so in the future.

-   **package.support.name**

    Specifies the person who provides support for the DITA-OT plug-in.

-   **package.support.email**

    Specifies the e-mail address of the person who provides support for the DITA-OT plug-in.

-   **package.version**

    Specifies the version of the DITA-OT plug-in.

    The value uses the following syntax:

    ```
    major.minor.micro.qualifier
    ```

    where:

    -   major is a number and is required.
    -   minor is a number and is optional.
    -   micro is a number and is optional.
    -   qualifier is optional and can be composed of numerals, uppercase or lower case letters, underscores, and hyphens.
    By default, the package.version value is set to `0.0.0`.


## Example

```
<plugin id="com.example.WithSupportInfo">
  <feature extension="package.support.name" value="Joe the Author"/>
  <feature extension="package.support.email" value="joe@example.com"/>
  <feature extension="package.version" value="1.2.3"/>
</plugin>
```

**Related information**  


[Extension points in org.dita.base](../extension-points/extension-points-in-org.dita.base.md)

