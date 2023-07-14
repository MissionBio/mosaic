
Changelog
=========

.. py:currentmodule:: missionbio.mosaic

v3.0.1
------
**Release date**: 2023-06-20

Added
~~~~~

* :meth:`assay._Assay.crosstab` to wrap ``pandas.crosstab`` for ease of use with mosaic.
* :meth:`assay._Assay.crosstabmap` to create heatmaps of the output of :meth:`assay._Assay.crosstab`.
* :meth:`assay._Assay.hierarchical_cluster` to get the hierarchical clustering order of the rows of a DataFrame.

Changed
~~~~~~~

* Updated matplotlib dependency from ``<=3.2.2`` to ``>=3.4.0``

Fixed
~~~~~

* :meth:`assay._Assay.heatmap` subclustering performed when `convolve=0`. It was disabled by default.
* Custom ``typography.css`` used in workflows is included in the package data
* Setting labels using dictionaries in :meth:`assay._Assay.set_labels`.

v3.0.0
------
**Release date**: 2023-06-16

Added
~~~~~

* A wrapper for COMPASS.
* New variant filters that account for missing data.
* Recipe and instructions for building installers.
* ``plot_kind`` parameter to :meth:`dna.Dna.group_by_genotype` to change the type of plot shown.
* ``filter_cells`` to :meth:`io.load` which loads only the intersection algorithm cells.
* Progress bar to :meth:`io.load`
* :class:`algorithms.nsp.NSP` and :class:`algorithms.nsp.ExpressionProfile` to modularize the NSP code.
* ``x_groups`` to :meth:`assay._Assay.heatmap` to group the x-axis by a given list of ids.
* Simplify and speedup :meth:`assay._Assay.heatmap` by removing duplicate data. (By using :class:`plots.heatmap.Heatmap`)
* :meth:`assay._Assay.convolve` to convolve the data that was earlier performed in the Heatmap.
* Configuration options accessible via :class:`Config`:

  * ``ms.Config.Colorscale.Dna`` to change the default color palette for all DNA plots.
  * ``ms.Config.Colorscale.Cnv`` to change the default color palette for all CNV plots.
  * ``ms.Config.Colorscale.Protein`` to change the default color palette for all Protein plots.

* Custom divirgent colorscale for Cnv Ploidy heatmaps
* Option to return indices instead of barcodes in :meth:`assay._Asasy.clustered_barcodes`.
* :meth:`sample.Sample.common_barcodes` to get the common barcodes across assays.
* Add ``subcluster`` paramter to :meth:`assay._Assay.clustered_barcodes` to prevent clustering within the labels
* Option to pass n-dimensional arrays as splitby in :meth:`assay._Assay.clustered_barcodes`
* Option to fetch a subset of the assays in :meth:`sample.Sample.assays` using the ``names`` parameter
* :meth:`sample.Sample.clustered_barcodes` to hierarchically cluster using multiple assays
* Multiple options added to :meth:`sample.Sample.heatmap` to sort the assays, barcodes, and the features
* :meth:`assay._Assay.signature`` accepts a ``splitby`` parameter to get the signature for each unique label in ``splitby``.
* Improvements to :meth:`assay._Assay.signaturemap`:

  * labels and ids are clustered by default.
  * Option to pass a list of labels to :meth:`assay._Assay.signaturemap` to order the labels.
  * The default ``features`` option for :meth:`cnv.Cnv.signaturemap` is set to ``positions``.

* Option to copy the labels and palette together by passing an :meth:`assay._Assay` to :meth:`assay._Assay.set_labels`
* :meth:`assay._Assay.heatmap` sets ``subcluster=False`` when calculating the barcode order when convolve is provided.
* Varsome URLs as hyperlinks on the variant name in the :class:`~workflows.variant_subclone_table.VariantSubcloneTable`
* Add percentage of cells and amplicons present to the :class:`~workflows.copy_number.CopyNumberWorkflow`
* :meth:`dna.Dna.mutated_cells` to get the number of cells with at least 1 mutation in each given clone. This is used in :meth:`sample.Sample.signaturemap`.

Changed
~~~~~~~

* ``apply_filter`` changed to ``filter_variants`` in :meth:`io.load`
* SubcloneTree and SubcloneTreeGraph classes are renamed to Tree and TreeGraph respectively.
* ``show_plot`` to ``return_plot`` in :meth:`dna.Dna.group_by_genotype`
* :class:`plots.heatmap.Heatmap` splits the vertical and horizontal lines on the main heatmap into two traces.
* The default value of ``vaf_het`` in :meth:`dna.Dna.filter_variants` changed from 35 to 30.
* Flattened :meth:`sample.Sample.heatmap`` option has been removed. A more customizable version is available under the :meth:`sample.Sample.signaturemap` function.
* The constant - :attr:`constants.COLORS` to have unique values.

  * The grey values at the 10th, 20th, 30th.. positions were modified to be unique
  * The black (``#000000``) value was moved from the 20th position to the last position

Fixed
~~~~~

* Get indexes maintains the order as per ``find_list`` when there are duplicates in the ``find_list`` and ``order_using_find_list`` is True.
* DANN score in the variants subclone table is shown correctly for saved h5 files.
* Overlapping of text in phylogeny trees.
* Error in multiprocessing when fetching gene_names for CNV by adding a ``max_workers`` parameter and using threads instead of processes.
* Missing clone is ignored when finding ADO sisters.

Removed
~~~~~~~

* Functions to convert legacy loom files to h5 files - ``io._loom_to_h5``, ``io._update_file``
* Functions to read data from csv files - ``io._merge_files``, ``io._cnv_raw_counts``, ``io._protein_raw_counts``
* Function to merge h5 files - ``io._merge``
* ``show_plot`` from :meth:`protein.Protein.normalize_reads`. The same plot can be created in plotly using :meth:`algorithms.nsp.NSP.plot`
* ``show_plot`` from :meth:`protein.Protein.get_signal_profile`. The same plot can be created in plotly using :meth:`algorithms.nsp.ExpressionProfile.plot`
* ``protein.Protein.get_signal_profile`` function. It can be executed using :meth:`algorithms.nsp.ExpressionProfile.fit` if needed.
* ``protein.Protein.get_scaling_factor`` function. It can be executed using :meth:`algorithms.nsp.NSP.scaling_factor` if needed
