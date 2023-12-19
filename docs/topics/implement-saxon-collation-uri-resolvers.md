# Implementing custom Saxon collation URI resolvers

Plug-ins can provide custom URI resolvers that provide collators for specific collation URIs.

To do custom sorting and grouping in XSLT, you identify collators using URIs that Saxon resolves to collator implementations. You implement the mapping from collation URIs to collators through custom collation URI resolvers.

For example, the DITA Community I18N plugin provides a custom collator for doing dictionary-based sorting and grouping of Simplified Chinese.

To allow multiple plug-ins to contribute collation URI resolvers, DITA-OT defines a superinterface of Saxon’s `CollationUriResolver` interface, `org.dita.dost.module.saxon.DelegatingCollationUriResolver`, that takes a base resolver.

Implementations of `DelegatingCollationUriResolver` should delegate to their base resolver if they do not resolve the URI specified on the resolve request. When multiple plug-ins provide resolvers it results in a chain of resolvers, ending with the built-in Saxon default resolver.

**Note:** The order in which plug-ins will be processed during collation URI resolver configuration is variable, so two plug-ins should not try to resolve the same collation URI. In that case the first one configured will be used at run time.

A typical delegating collation URI resolver looks like this:

```language-java
public class DCI18nCollationUriResolver implements DelegatingCollationUriResolver {

  public static final String DITA_COMMUNITY_I18N_ZH_CNAWARE_COLLATOR =
      "http://org.dita-community.i18n.zhCNawareCollator";
  public static final String LANG_URI_PARAM = "lang";

  private CollationURIResolver baseResolver;

  public DCI18nCollationUriResolver() {
      super();
      this.baseResolver = StandardCollationURIResolver.getInstance();
  }


  public net.sf.saxon.lib.StringCollator resolve(String uri, Configuration configuration) 
          throws XPathException {
      ZhCnAwareCollator collator = resolveToZhCnAwareCollator(uri, null, configuration);
      if (null == collator) {
          return baseResolver.resolve(uri, configuration);
      }
      return (StringCollator) collator;
  }


  @Override
  public void setBaseResolver(CollationURIResolver baseResolver) {
    this.baseResolver = baseResolver;
  }
  
  /* ... Code to evaluate the collation URI and provide the appropriate collator goes here */
}
```

To implement a custom collation URI resolver:

1.  Add your plugin’s JAR file in the DITA-OT class path as described in [Adding a Java library to the classpath](plugin-javalib.md).
2.  Implement an instance of `org.dita.dost.module.saxon.DelegatingCollationUriResolver` as described above.
3.  Include a file named `org.dita.dost.module.saxon.DelegatingCollationUriResolver` in the directory `META-INF/services` in the compiled JAR that your plug-in provides. Each line of the file must be the name of a class that implements `org.dita.dost.module.saxon.DelegatingCollationUriResolver`:

    ```
    org.example.i18n.saxon.MyCollationUriResolver
    ```

    You can create the services file using `<service>` elements in an Ant `<jar>` task:

    ```language-xml
    <jar destfile="${basedir}/target/lib/example-saxon.jar">
      [...]
      <service type="org.dita.dost.module.saxon.DelegatingCollationUriResolver">
        <provider classname="org.example.i18n.saxon.MyCollationUriResolver"/>
      </service>
      [...]
    </jar>
    ```

4.  To use the collator in XSLT style sheets, specify the collation URI on `@xsl:sort` elements \(or anywhere a collator URI can be specified\):

    ```language-xml
    <xsl:apply-templates select="word">
      <xsl:sort collation="http://org.example.i18n.MyCollator"/>
    </xsl:apply-templates>
    ```


**Related information**  


[DITA Community](https://www.oxygenxml.com/events/2015/dita-ot_day.html#DITA_Community)

