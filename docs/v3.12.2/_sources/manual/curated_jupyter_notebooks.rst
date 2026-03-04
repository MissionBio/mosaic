.. _curated_jupyter_notebooks:

Curated Jupyter Notebooks
-------------------------

A collection of Jupyter notebooks with established workflows for analysing DNA only and DNA+Protein
Tapestri runs. They contain a detailed explanation of every step from loading the h5 file to saving
and exporting the analysis results. These workflows can be used for standard analysis. For more
advanced analysis, please refer to the :ref:`vignettes` section of the documentation.

.. note::

   The notebooks can be downloaded using the `Download` button on the top right corner
   of the notebook's page

.. list-table:: Notebooks
   :widths: 40 60
   :header-rows: 1

   * - Notebook Link
     - Description
   * - DNA_
     - Dna analysis notebook. It also covers CNV.
   * - `Multisample DNA`_
     - Multisample analysis notebook. Each sample must be related to the other.
       For example, multiple time points of the same patient.
   * - `DNA+Protein`_
     - DNA and Protein analysis.
   * - `Multisample DNA+Protein`_
     - Multisample DNA and Protein analysis. The samples must be related to each other.

.. _DNA: ../notebooks/curated_notebooks/dna.html
.. _Multisample DNA: ../notebooks/curated_notebooks/dna-multisample.html
.. _DNA+Protein: ../notebooks/curated_notebooks/dna-protein.html
.. _Multisample DNA+Protein: ../notebooks/curated_notebooks/dna-protein-multisample.html

.. toctree::
   :hidden:
   :maxdepth: 1

   ../notebooks/curated_notebooks/dna
   ../notebooks/curated_notebooks/dna-multisample
   ../notebooks/curated_notebooks/dna-protein
   ../notebooks/curated_notebooks/dna-protein-multisample