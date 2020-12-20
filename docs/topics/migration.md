# Migrating customizations

If you have XSL transformation overrides, plug-ins or other customizations written prior to DITA-OT 3.6, you may need to make changes to ensure your overrides work properly with the latest toolkit versions.

In some cases, you may be able to remove old code that is no longer needed. In other cases, you may need to refactor your code to point to the modified extension points, templates or modes in recent toolkit versions.

When migrating customizations, identify the version of the toolkit you're currently using \(base version\) and the version of the toolkit you want to migrate to \(target version\). Then, review all of the migration changes described in *all* of the versions from the base through the target. For instance, if you're currently on 2.2 and want to move to 3.3, you should review all of the changes in 2.3 through 3.3. You may want to start at the oldest version and read forward so you can chronologically follow the changes, since it is possible that files or topics have had multiple changes.

**Note:**

DITA-OT releases follow [semantic versioning](https://semver.org) guidelines. Version numbers use the `major.minor.patch` syntax, where major versions may include incompatible API changes, minor versions add functionality in a backwards-compatible manner and patch versions are maintenance releases that include backwards-compatible bug fixes.

Custom plug-ins developed for a previous major version may require changes to work correctly with recent toolkit versions. Most plug-ins should be compatible with subsequent minor and patch versions of the major release for which they were originally developed.

**Related information**  


[Gotcha! Upgrading PDF plugins to DITA-OT 2.x](https://www.oxygenxml.com/events/2016/dita-ot_day.html#Upgrading_PDF_plugins_to_DITA_OT_2.x)

