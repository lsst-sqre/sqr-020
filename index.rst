:tocdepth: 1

.. Please do not modify tocdepth; will be fixed when a new Sphinx theme is shipped.

.. sectnum::

.. note::

   **This technote is a work in progress.**

   This technote explores how JSON-LD (Linked Data) can be used to describe a variety of LSST project artifacts, including source code and documents. We provide specific examples using standard vocabularies (http://schema.org and CodeMeta) and explore whether custom terms are needed to support LSST use cases.

Technotes
=========

Technotes are documents published by LSST as websites.
Technotes are also software-like, with code repositories and continuous integration services.

Technote as a Report type
-------------------------

To simply describe a technote as a document, we can use the schema.org `Report`_ type.
`Report`_ extends both the `Article`_ and `CreativeWork`_ types, and specifically provides a reportNumber_ field.
We'll use that reportNumber_ field to hold the technote's handle, such as ``SQR-020`` for this technote.

This example shows how `SQR-006`_ can be described in JSON-LD as a schema.org `Report`_:

.. literalinclude:: examples/sqr-006.jsonld
   :language: json

`Report`_ types allow for more terms that we've used here.
For example, the articleBody_ field can contain the full plain-text contents of the document.
This could be useful for full-text search services.

Technote with additional SoftwareSourceCode terms
-------------------------------------------------

Technotes are also code, as we mentioned previously.
We can incorporate metadata about the technote's underlying code infrastructure by adding the schema.org `SoftwareSourceCode`_ type.
JSON-LD allows nodes to have an array of types, so that our technote can effectively become both a document and a code project, with terms from both types.

For code projects, we can also use the expanded `term vocabulary from the CodeMeta project`_.
CodeMeta and SoftwareSourceCode_ provide these terms, (among others):

- programmingLanguage_. Name of the dominant programming language. We should use GitHub Linguist's languages.yml_ as a controlled vocabulary for language names.
- `codeRepository`_. Link to the GitHub repository.
- ``contIntegration`` (CodeMeta). URL of the continuous integration service dashboard.
- ``readme`` (CodeMeta): URL of the README file.
- ``developmentStatus`` (CodeMeta): Description of development status. Use terms from http://repostatus.org.
- ``maintainer`` (CodeMeta): the Person_ that is responsible for maintaining the repository.

This example shows `SQR-006`_ described as a combined Report_ and SoftwareSourceCode_:

.. literalinclude:: examples/sqr-006.softwaresourcecode.jsonld
   :language: json

.. .. rubric:: References

.. Make in-text citations with: :cite:`bibkey`.

.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :encoding: latex+latin
..    :style: lsst_aa

.. _SQR-006: https://sqr-006.lsst.io
.. _`term vocabulary from the CodeMeta project`: https://codemeta.github.io/terms/
.. _languages.yml: https://github.com/github/linguist/blob/master/lib/linguist/languages.yml
.. _Person: http://schema.org/Person
.. _Report: http://schema.org/Report
.. _Article: http://schema.org/Article
.. _CreativeWork: http://schema.org/CreativeWork
.. _SoftwareSourceCode: http://schema.org/SoftwareSourceCode
.. _articleBody: https://schema.org/articleBody
.. _reportNumber: https://schema.org/reportNumber
.. _codeRepository: https://schema.org/codeRepository
.. _programmingLanguage: https://schema.org/programmingLanguage
