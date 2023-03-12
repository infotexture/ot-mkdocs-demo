# Building output using Ant

You can build output by using an Ant build script to provide the DITA-OT parameters.

1.  Open a command prompt or terminal session.

2.  Issue the following command:

        |**Linux or macOS **|bin/ant -f `build-script target`|
    |**Windows**|bin\\ant -f `build-script target`|

    where:

    -   build-script is name of the Ant build script.
    -   target is an optional switch that specifies the name of the Ant target that you want to run.

        If you do not specify a target, the value of the `@default` attribute for the Ant project is used.


**Related information**  


[Migrating Ant builds to use the dita command](../topics/migrating-ant-to-dita.md)

[Ant](../topics/ant.md)

[DITA-OT parameters](../parameters/parameters_intro.md)

[Apache Ant documentation](http://ant.apache.org/manual)

