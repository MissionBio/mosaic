Welcome
=======

.. note::

    Documentation for v1.8.0 can be found `here <https://missionbio.github.io/mosaic/v1.8.0/index.html>`_

Mosaic is a set of tools to analyze DNA and protein data obtained from the Mission Bio Tapestri instrument.

.. toctree::
    :maxdepth: 2

    1_introduction
    2_install
    3_getting_started
    4_data_structure

* :ref:`genindex`

.. _all-vignettes:

Vignettes
---------

.. toctree::
    :maxdepth: 2

    examples/index
    examples/basics.ipynb
    examples/cnv.ipynb
    examples/filtering.ipynb
    examples/customizations.ipynb
    examples/multi-sample-analysis.ipynb
    examples/additional-plots-and-customizations.ipynb
    examples/analysis-walkthrough.ipynb

Interface
---------

.. rubric:: Modules

.. autosummary::
   :recursive:
   :caption: Modules
   :toctree: pages
   :template: module.rst

   ~missionbio.mosaic.io
   ~missionbio.mosaic.utils
   ~missionbio.mosaic.constants


.. rubric:: Classes

.. autosummary::
   :recursive:
   :nosignatures:
   :caption: Classes
   :toctree: pages
   :template: class.rst

   ~missionbio.mosaic.assay._Assay
   ~missionbio.mosaic.dna.Dna
   ~missionbio.mosaic.cnv.Cnv
   ~missionbio.mosaic.protein.Protein
   ~missionbio.mosaic.sample.Sample
   ~missionbio.mosaic.samplegroup.SampleGroup
