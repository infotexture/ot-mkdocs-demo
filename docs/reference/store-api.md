# Store API – Processing in memory

DITA-OT originally assumed resources would be available on disk and available from file paths. Recent versions added URI input, so HTTPS resources could be used, but temporary and output resources were still file-based. DITA-OT 3.6 introduces a new Store API that can process temporary resources in memory instead of writing them to disk.

The Store API \(`org.dita.dost.store.Store`\) is a Java abstraction over temporary file operations. So for example instead of reading resources directly with `FileInputStream`, the Store API provides operations for this. This abstraction allows implementations of the Store API to choose how they handle resources, enables optimizations or non–file-based storage. Since DITA-OT processes a lot of XML data, the Store API offers operations for XML processing directly. For example, a read method to directly get a DOM `Document`, instead of opening a file stream manually, parsing it with an XML parser, and getting the `Document` instance from the parser.

The Store API is extendable using Java’s [Resource Loader](https://docs.oracle.com/javase/9/docs/api/java/util/ServiceLoader.html) with the `org.dita.dost.store.StoreBuilder` service. This is a builder interface to get named `Store` instances \(“a Store”\).

## Stream Store for file-based processing

This Store could also be a File Store, since it uses disk and local files for temporary resources. This is the traditional DITA-OT implementation, where temporary XML files are stored under the `dita.temp.dir` path.

The Stream Store is activated by setting the store-type parameter to file.

**Note:** To ensure backwards compatibility, the file Store is the default setting in DITA-OT 3.6.

## Cache Store for in-memory processing

This Store is an in-memory Store, that keeps all temporary resources in memory. The name comes from the feature of the Store, that it caches the parsed XML after reading. That is, instead of storing XML as a byte array, it keeps it as a DOM `Document` or S9api `XdmNode`. When the same resource is re-read later, it doesn't have to parse it again, only return the parsed document. Resources that are not available in the temporary directory are handled with the Stream Store.

While the Store doesn't write anything to the temporary directory, it will still use URIs where the resources are under the temporary directory. The URIs are simply used for addressing, similarly to URNs. Future releases of DITA-OT may use some other method of addressing, such as a `tmp` URI scheme.

**Tip:** As of DITA-OT 3.6, the Cache Store can be activated by setting the store-type parameter to memory.

## Benefits

The initial implementation of the Cache Store is provided in DITA-OT 3.6 as a preview to allow integration partners to test this new feature.

In-memory processing provides performance advantages in I/O bound environments such as cloud computing platforms, where processing time depends primarily on how long it takes to read and write temporary files.

The Store API also makes the Saxon S9api easier to use. It offers an XML document model that is in most cases easier to work with than DOM. The abstraction Store makes it easier to work with XML, so various modules don’t need to repeat the same type of XML processing code.

## Caveats

Not all custom plug-ins will work with the Cache Store, because they may assume files are used and expect direct file access for resource operations.

**Important:** To take advantage of the Store API, custom plug-ins must use DITA-OT XSLT modules in custom `pipeline` elements instead of Ant’s built-in `xslt` tasks as recommended in [Plug-in coding conventions](../topics/plugin-coding-conventions.md).

