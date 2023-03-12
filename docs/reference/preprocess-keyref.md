# Resolve key references \(`keyref`\)

The `keyref` step examines all the keys that are defined in the DITA source and resolves the key references. Links that make use of keys are updated so that any `@href` value is replaced by the appropriate target; key-based text replacement is also performed. This step is implemented in Java.

