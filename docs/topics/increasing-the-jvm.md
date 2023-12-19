# Increasing Java memory allocation

If you are working with large documents with extensive metadata or key references, you will need to increase the memory allocation for the Java process. You can do this from the command-line prompt for a specific session, or you can increase the value of the `ANT_OPTS` environment variable.

-   To change the value for a specific session, from the command prompt, issue the following command:

    |Platform|Command|
    |--------|-------|
    |**Linux or macOS **|`export ANT_OPTS=$ANT_OPTS -Xmx*1024*M`|
    |**Windows**|`set ANT_OPTS=%ANT_OPTS% -Xmx*1024*M`|

    This increases the JVM memory allocation to 1024 megabytes. The amount of memory which can be allocated is limited by available system memory and the operating system.

-   To persistently change the value, change the value allocated to the `ANT_OPTS` environment variable on your system.


