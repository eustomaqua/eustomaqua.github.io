.. eustomaqua documentation master file, created by
   sphinx-quickstart on Fri Jul 31 14:06:56 2026.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to MkDocs
========================

Add your content using ``reStructuredText`` syntax. See the
`reStructuredText <https://www.sphinx-doc.org/en/master/usage/restructuredtext/index.html>`_
documentation for details.


.. toctree::
   :maxdepth: 2
   :caption: Contents:


.. code-block:: shell

  source activate py3e

  mkdocs new docs
  cd docs
  mkdocs build
  mkdocs serve

  sphinx-quickstart
  > Separate source and build directories (y/n) [n]: y
  > Project name: eustomaqua
  > Author name(s): eustomaqua
  > Project release []: 0.1
  > Project language [en]: en
  make html
