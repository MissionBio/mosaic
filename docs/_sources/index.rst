Mosaic API documentation
========================

.. admonition:: Older documentations
   :class: note

   The latest version of Mosaic is recommended for new developments. Documentation for the other
   versions are available for applications and notebooks built using them:
   `v3.7.0r1 (first documentation revision of v3.7.0) <https://missionbio.github.io/mosaic/v3.7.0r1/index.html>`_
   , `v3.4.0 <https://missionbio.github.io/mosaic/v3.4.0/index.html>`_
   , `v3.1.1 <https://missionbio.github.io/mosaic/v3.1.1/index.html>`_
   , `v2.4.1 <https://missionbio.github.io/mosaic/v2.4.1/index.html>`_
   , `v1.8.0 <https://missionbio.github.io/mosaic/v1.8.0/index.html>`_


Mosaic is a set of tools to analyze DNA and protein data obtained from the Mission Bio Tapestri instrument.
Its designed to allow convenient handling and visualization of single-cell multiomics data to enable
exploratory analysis.

.. The following are not shown on this page, but are used to generate the sidebar navigation
.. toctree::
   :hidden:
   :maxdepth: 2

   manual/install
   manual/getting_started
   manual/data_structure
   manual/vignettes
   manual/curated_jupyter_notebooks
   manual/help
   manual/changelog

Basic Classes
~~~~~~~~~~~~~
.. autosummary::
   :recursive:
   :nosignatures:
   :caption: Basic Classes
   :toctree: pages
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
   :toctree: pages
   :template: class.rst

   ~missionbio.mosaic.workflows.copy_number.CopyNumber
   ~missionbio.mosaic.workflows.variant_subclone_table.VariantSubcloneTable

Algorithms
~~~~~~~~~~
.. autosummary::
   :recursive:
   :caption: Algorithms
   :toctree: pages
   :template: class.rst

   ~missionbio.demultiplex.protein.nsp.NSP
   ~missionbio.mosaic.algorithms.group_by_genotype.GroupByGenotype
   ~missionbio.mosaic.algorithms.compass.COMPASS

Functional Modules
~~~~~~~~~~~~~~~~~~
.. autosummary::
   :recursive:
   :caption: Functional Modules
   :toctree: pages
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
   :toctree: pages
   :template: class.rst

   ~missionbio.plotting.heatmap.Heatmap
   ~missionbio.plotting.lineplot.LinePlot
   ~missionbio.plotting.bargraph.BarGraph
   ~missionbio.plotting.multimap.MultiMap
   ~missionbio.plotting.phylotree.PhyloTree
   ~missionbio.plotting.fishplot.Fishplot

DNA Assignment
~~~~~~~~~~~~~~
.. autosummary::
   :recursive:
   :nosignatures:
   :caption: DNA assignment
   :toctree: pages
   :template: class_all_attrs.rst

   ~missionbio.demultiplex.dna.truth.Truth
   ~missionbio.demultiplex.dna.likelihood.LikelihoodMethod
   ~missionbio.mosaic.algorithms.dna_assignment.DnaAssignment

Protein Assignment
~~~~~~~~~~~~~~~~~~
.. autosummary::
   :recursive:
   :nosignatures:
   :caption: Protein assignment
   :toctree: pages
   :template: class_all_attrs.rst

   ~missionbio.demultiplex.protein.truth.Truth
   ~missionbio.demultiplex.protein.pace.likelihood.LikelihoodMethod
   ~missionbio.demultiplex.protein.pace.probability.ProbabilityMethod