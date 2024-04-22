.. _vignettes:

Vignettes
---------

For standard analysis see :ref:`curated_jupyter_notebooks`.

This is a collection of Jupyter notebooks demonstrating the use of the `mosaic` package. These
are not meant to be representative of all the functionality of the package, but rather
to provide a starting point for users to explore the package and its capabilities. The notebooks
are meant to be read in the order they are listed below, as they build on each other. The objective
is to explain the package architecture to enable the user  to create their own custom plots
and workflows.

.. note::

   :meth:`~missionbio.mosaic.io.load_example_dataset` is used in various vignettes. This
   downloads a small example dataset from the Mission Bio GitHub. It can be replaced with
   :meth:`~missionbio.mosaic.io.load` to load a dataset from a local directory.

.. list-table:: Notebooks
   :widths: 40 60
   :header-rows: 1

   * - Vignette Link
     - Description
   * - Overview_
     - Overview of the package and its functionality
   * - Filtering_
     - Filtering the data and plotting the results
   * - CNV_
     - Plotting copy number data
   * - `Plot customizations`_
     - Options to customize the plots
   * - `Multi sample analysis`_
     - Performing multi-sample analysis
   * - `Additional plots and code`_
     - Additional plots not directly available in mosaic.
   * - `Code snippets`_
     - Snippets of code showcasing various features of the package

.. _Overview: ../notebooks/overview.html
.. _Filtering: ../notebooks/filtering.html
.. _CNV: ../notebooks/cnv.html
.. _Plot customizations: ../notebooks/plot-customizations.html
.. _Multi sample analysis: ../notebooks/multi-sample-analysis.html
.. _Additional plots and code: ../notebooks/additional-plots-and-customizations.html
.. _Code snippets: ../notebooks/code-snippets.html

.. toctree::
   :hidden:
   :maxdepth: 1

   ../notebooks/overview
   ../notebooks/filtering
   ../notebooks/cnv
   ../notebooks/plot-customizations
   ../notebooks/multi-sample-analysis
   ../notebooks/additional-plots-and-customizations
   ../notebooks/code-snippets