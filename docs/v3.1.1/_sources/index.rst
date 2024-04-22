Mosaic API documentation
========================

.. admonition:: Older documentations
   :class: note

   The latest version of Mosaic is recommended for new developments. Documentation for the other
   versions are available applications and notebooks built using them:
   `v2.4.1 <https://missionbio.github.io/mosaic/v2.4.1/index.html>`_
   & `v1.8.0 (unsupported) <https://missionbio.github.io/mosaic/v1.8.0/index.html>`_


Mosaic is a set of tools to analyze DNA and protein data obtained from the Mission Bio Tapestri instrument.
Its designed to allow convenient handling and visualization of single-cell multiomics data to enable
exploratory analysis.

.. The following are not shown on this page, but are used to generate the sidebar navigation
.. toctree::
   :hidden:
   :maxdepth: 2

   pages/install
   pages/getting_started
   pages/data_structure
   pages/vignettes
   pages/curated_jupyter_notebooks
   pages/help
   pages/changelog

Basic Classes
~~~~~~~~~~~~~
.. autosummary::
   :recursive:
   :nosignatures:
   :caption: Basic Classes
   :toctree: autosummary_pages
   :template: class.rst

   ~missionbio.mosaic.assay._Assay
   ~missionbio.mosaic.dna.Dna
   ~missionbio.mosaic.cnv.Cnv
   ~missionbio.mosaic.protein.Protein
   ~missionbio.mosaic.sample.Sample
   ~missionbio.mosaic.samplegroup.SampleGroup

Interactive Workflows
~~~~~~~~~~~~~~~~~~~~~
.. autosummary::
   :recursive:
   :nosignatures:
   :caption: Interactive Workflows
   :toctree: autosummary_pages
   :template: class.rst

   ~missionbio.mosaic.workflows.copy_number.CopyNumber
   ~missionbio.mosaic.workflows.variant_subclone_table.VariantSubcloneTable

Algorithms
~~~~~~~~~~
.. autosummary::
   :recursive:
   :caption: Algorithms
   :toctree: autosummary_pages
   :template: class.rst

   ~missionbio.mosaic.algorithms.nsp.NSP
   ~missionbio.mosaic.algorithms.group_by_genotype.GroupByGenotype
   ~missionbio.mosaic.algorithms.compass.COMPASS

Functional Modules
~~~~~~~~~~~~~~~~~~
.. autosummary::
   :recursive:
   :caption: Functional Modules
   :toctree: autosummary_pages
   :template: module.rst

   ~missionbio.mosaic.io
   ~missionbio.mosaic.utils
   ~missionbio.mosaic.constants

Custom Plots
~~~~~~~~~~~~
.. autosummary::
   :recursive:
   :nosignatures:
   :caption: Custom Plots
   :toctree: autosummary_pages
   :template: class.rst

   ~missionbio.mosaic.plots.heatmap.Heatmap
   ~missionbio.mosaic.plots.lineplot.LinePlot
   ~missionbio.mosaic.plots.bargraph.BarGraph
   ~missionbio.mosaic.plots.multi_heatmap.MultiHeatmap
   ~missionbio.mosaic.plots.fishplot.TreeGraph
   ~missionbio.mosaic.plots.fishplot.Fishplot
