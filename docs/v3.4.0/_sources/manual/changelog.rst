
Changelog
=========

.. py:currentmodule:: missionbio.mosaic

v3.4.0
------
**Release date**: 2024-04-01

Added
~~~~~

* Support to pass ``x_groups`` to :meth:`~sample.Sample.signaturemap` and :meth:`~sample.Sample.heatmap`.
* Support to pass variant filters to :meth:`~io.load`.
* :meth:`~cnv.Cnv.positions`, :meth:`~cnv.Cnv.amplicon_performance`, & :meth:`~cnv.Cnv.panel_uniformity` to quickly get amplicon positions, performance and panel uniformity.
* Option to hide columns in the variants table of the :class:`~workflows.variant_subclone_table.VariantSubcloneTable` workflow.
* Ability to filter variants through the GUI in the :class:`~workflows.variant_subclone_table.VariantSubcloneTable` workflow.
* ``override`` parameter for the :meth:`~assay._Assay.heatmap` function which is simply passed to ``clustered_ids`` and ``clustered_barcodes``.
* The first column of the subclone table is frozen.
* Mandate ``features`` when ``x_groups`` is provided in :meth:`~assay._Assay.heatmap`.
* An appropriate error is raised when any cell has 0 total reads when running ``NSP``.
* An appropriate error is raised when the annotation API is not available.

Changed
~~~~~~~

* Increased the vertical spacing between the graph and the fishplot from 0 to 0.1.
* The plotting functions in ``missionbio.mosaic.plotting`` were moved to ``missionbio.plotting``
* ``missionbio.algorithms.nsp`` was moved to ``missionbio.demultiplex.protein.nsp``
* Unpinned ``scikit-learn`` and ``hdbscan`` as their latest versions are compatible with each other.
* ``scikit-learn>1.3.1`` is installed by default which results in slightly different NSP calls due to changes to its Gaussian mixture model.

Fixed
~~~~~

* Load the whitelist variants correctly when ``filter_variants=True`` is passed to :meth:`~io.load`.
* Nill values of DANN score are shown as empty cells instead of ``º``.
* :meth:`~cnv.Cnv.name_id_by_pos` does not filter the amplicons.
* Lineplot in :meth:`~cnv.Cnv.plot_ploidy` does not connect the medians with a line when using ``genes+amplicons`` or ``positions+amplicons``.
* The violin plot range is fixed to (0, 100) for the ``AF`` and ``GQ`` layers in :class:`~workflows.variant_subclone_table.VariantSubcloneTable`.
* Violin plots generated using :meth:`~assay._Assay.violinplot` are equally spaced when split by labels.
* Fix resetting of ``selected_bars`` when scatterplots are created.
* :meth:`~assay._Assay.rename_labels` allows swapping of labels.
* Fishplot does not disappear when a clone and its parent both have 0 cells at some timepoint.

v3.1.1
------
**Release date**: 2023-09-25

Added
~~~~~
* Relaxed missionbio.h5 requirement to >=4.13.0,<6

Changed
~~~~~~~

* Disable autouploading of tagged packages to anaconda.
* Removed check for h5 file compatibility with H5Reader.

Fixed
~~~~~

* The ``whitelist`` option in :meth:`~io.load` correctly loads exact matches of variants.

v3.1.0
------
**Release date**: 2023-09-13

Added
~~~~~

* The order of the names in the legend matches the order of the traces in the ridgeplot.
* Option to pass any sequence type to :meth:`~assay._Assay.get_attribute` besides np.ndarray. This includes list, tuple, and range.
* ``features`` parameter to :meth:`~assay._Assay.signature` which allows grouping across ids, just like ``splitby`` allows grouping across cells.
  * The ``feautures`` option in :meth:`~assay._Assay.signaturemap` allows plotting using grouped data from :meth:`~assay._Assay.signature`
* Support for hg38 along with all species available through Ensembl in :meth:`~cnv.Cnv.get_annotations`
* Support for hg38 in :meth:`~dna.Dna.get_annotations`.
* Sped up NSP by 2x by using ``statsmodels`` for the KDE and using spherical covariance with kmeans++ initialization for the GMM parameters.
* ``ANSP`` - Approximate NSP to protein normalization. It runs in constant time for large datasets.
* :meth:`~assay._Assay.get_attribute` also accepts dataframes.
* :meth:`~assay._Assay.heatmap` can plot arbitrary dataframes as long as it has the expected number of cells.
* ``TreeGraph`` now supports html tags like ``<br>``, ``<b>``, and ``<span>`` in the descriptions.

Changed
~~~~~~~

* Use latest python 3.8 in installer instead of 3.8.0

Fixed
~~~~~

* The title of :meth:`~sample.Sample.clone_vs_analyte` plot does not overlap with the DNA heatmap.
* The x-axis label order for CNV in the :meth:`~sample.Sample.clone_vs_analyte` plot matches the order of the points in the data shown.
* NGT layer not modified after running :meth:`~dna.Dna.filter_variants`
* "Last modified" timestamp does not change when loading an H5 file.
* ``jitter`` parameter in ``NSP`` works
* Failure of :class:`~workflows.variant_subclone_table.VariantSubcloneTable` when all the variant calls are filtered.
* Pinned hdbscan to v0.8.29. Higher versions (>=0.8.30,<=0.8.33) have runtime issues.
* :meth:`~sample.Sample.heatmap` and :meth:`~sample.Sample.signaturemap` execute successfully when "cnv" is passed before "dna".
* Fix y-compression of ``TreeGraph`` by checking the upwards and downwards movement of only the highest and lowest nodes respectively.

Updated
~~~~~~~

* Switched from using the depracated JupyterDash to the builtin jupyter dash in Dash v2.11. `Documentation <https://dash.plotly.com/dash-in-jupyter>`_
* ``jupyter_client`` from <8 to >=8.1.0 as the ThreadedZMQStream error is fixed in it. `Changelog <https://jupyter-client.readthedocs.io/en/stable/changelog.html#id6>`_


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
