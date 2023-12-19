# History of the PDF transformation

The DITA Open Toolkit PDF transformation was originally based on a third-party contribution by Idiom Technologies, and is commonly known as the “pdf2” plug-in.

When IBM developed the code that later became DITA-OT, it included only a proof-of-concept PDF transformation. IBM had their own processing chain for producing PDFs from SGML, which they had developed over several decades, so resources were focused primarily on XHTML output and preprocessing.

Since the initial proof-of-concept transformation was not robust enough for production-grade output, companies began to develop their own PDF transformations. One company, Idiom Technologies, made their transformation \(known as the “pdf2” transformation\) available as open source on 23 February 2006. The Idiom plug-in was initially available as a separately-downloadable plug-in that could be installed into DITA-OT.

Later the DITA-OT project formally incorporated the Idiom plug-in as a demonstration in the `demo/fo` directory. Beginning with DITA-OT version 1.5, released 18 December 2009, the “pdf2” code served as the main, supported PDF transformation. \(The original PDF transformation was deprecated and renamed “legacypdf”.\) In DITA-OT version 1.6, the “pdf2” plug-in was moved to `plugins/org.dita.pdf2`.

The fact that the current PDF transformation was not originally developed in parallel with the other core DITA-OT transformations led to anomalies that often confuse users:

-   Elements are often \(by default\) styled differently in the XHTML and PDF transformations. For example, consider the `<info>` element in a task topic. In HTML output, this is an inline element; in PDF output, it is a block-level element.
-   The auto-generated strings used for localization are different, and so languages that are supported by DITA-OT differ based on whether the XHTML or PDF transformation is used.
-   The Idiom plug-in used its own extension mechanism \(the `Customization` folder\) to provide overrides to the PDF transformation.
-   Before the release of DITA 1.1 \(which added support for the indexing domain\), Idiom developed an index extension that used a FrameMaker-inspired syntax.

