
Changelog
=========

.. py:currentmodule:: missionbio.mosaic

v3.12.0
-------
**Release date**: 2025-21-04


Added
~~~~~

A new attribute for all assays: ``info``. This can be used to store arbitrary information of various types including pandas dataframes and dictionaries.
Unlike row attributes, column attributes, and layers, it is not confined to any shape. For example, the signature of the clones generated for only
the somatic variants would have fewer columns than ids and fewer rows than cells in the assay. Compass stores a lot information in it's variables,
until now there was no easy way of saving it in the h5. These are dataframes with shapes that do not align with that of the assay. These values can
now be stored in the assay ``info`` as follows:

>>> sample.dna.add_info("somatic_signature", compass.node_genotypes_)
>>> sample.dna.add_info("assignment_probability", compass.probability_)

The assays also now store their palette in the info as a dictionary. :meth:`~assay._Assay.sampleinfo` is a shortcut for accessing info for single sample assays.

>>> sample.dna.sampleinfo["palette"]

The functions for handling info are :meth:`~assay._Assay.has_info`, :meth:`~assay._Assay.add_info`, and :meth:`~assay._Assay.del_info`

**Updates to COMPASS**

* Update to the latest version of `COMPASS <https://github.com/MissionBio/compass/tree/e3e0169bbe52555b751752699cb22399c1b70763>`_
* Add option to rename compass clones with a new probability value using :meth:`~algorithms.compass.COMPASS.relabel`.
* Allow passing prefixes for file names to :meth:`~algorithms.compass.COMPASS.run`
* Added option to get fractions of each clone using :meth:`~algorithms.compass.COMPASS.node_fractions`
* Allow passing directories to :meth:`~algorithms.compass.COMPASS.run`
* COMPASS can call LOH clones without calling CNV using the ``cnv`` parameter in :meth:`~algorithms.compass.COMPASS.run`.

**Plotting updates**

* Cytoband information added to the CNV ploidy :meth:`~cnv.Cnv.signaturemap` and :meth:`~cnv.Cnv.plot_ploidy` figures. These are also shown in the CopyNumber workflow.
* ``ticks`` option to :meth:`~assay._Assay.heatmap` to disable plotting of ticks for assay with large number of ids.
* The scatterplot size modifies depending on the length of the labels to ensure that the plotting area is constant.

**Updates to CNV**

* Locally stored gene name annotations are used instead of pulling them from Ensembl when running :meth:`~cnv.Cnv.get_gene_names`.
* When using :meth:`~cnv.Cnv.get_gene_names`, the gene name will always be the best match for the amplicon instead of mutliple values separated by a ``/``
* :meth:`~cnv.Cnv.get_gene_names` returns the gene names while also adding it to the column attributes.

**Updates to DNA**

* :meth:`~dna.Dna.get_annotated_ids` returns a list of human-readable names for all the variants in the assay.
* :meth:`~dna.Dna.set_annotated_ids` updates the ids to be human-readable names.
* :meth:`dna.Dna.genome` to easily access the `genome_version` metadata value.
* Store annotations in the DNA assay `info` instead of the column attributes to ease their access.
* :meth:`dna.Dna.snps` to quickly get the ids that are SNPs.

**Functionality updates**

* Option to disable matching of ids in :class:`~samplegroup.SampleGroup` using the ``match_ids`` parameter.
* Ability to load h5 files with only raw counts.
* `whitelist=[]` is treated just like `whitelist=None` in :meth:`~io.load`
* Deduplication of barcodes is done using integers instead of sample names and no warning is raised when deduplication of barcodes is performed.
  It can be manually performed using :meth:`~assay._Assay.deduplicate_barcodes` and inverted using :meth:`~assay._Assay.normalize_barcodes`.
* Store the palette in the `info` instead of the metadata of the assay, making saved h5 files valid in format even with the stored palette.
* :attr:`sample.Sample.vdj` to easily access the VDJ assay in the h5 file.

Fixed
~~~~~
* ADO score shown in the figure is the same as the ADO score shown in the table in the :class:`~workflows.variant_subclone_table.VariantSubcloneTable` workflow
* Use the correct genome version from the dna assay in :class:`~algorithms.compass.COMPASS`
* :class:`~dna.Dna.get_annotations` raises an appropriate error when the genome version is not supported.


v3.7.0
------
**Release date**: 2024-08-05

Added
~~~~~

* :meth:`~dna.Dna.filter_somatic_variants()` for automatic filtering of pathogenic somatic variants.
* :meth:`dna.Dna.assign_from_truth` to label the cells for a known set of clones.
* :meth:`protein.Protein.cluster_and_label` to find all protein clusters and label them based on the provided truth. This function can be used to novel cell types.
* :meth:`protein.Protein.label_sticky_cells` to mark cells which are likely to be sticky.
* :meth:`protein.Protein.assign_from_truth` label the cells for a known set of cell types. By default, it labels the PBMC subtypes.
* :meth:`protein.Protein.truth` to convert cluster signatures to a truth that can be used for :meth:`~protein.Protein.assign_from_truth`
* Ability to pass an external control to :meth:`~cnv.Cnv.compute_ploidy`
* :meth:`~protein.Protein.read_depth_dependence` - a plot to quickly visualize the need and effectiveness of NSP normalization.
* Option to load a subset of the assays in the h5 file.
* No error is raised when h5 files with unknown assays are loaded.
* Raise an error when the number of variants to annotate is more than 1,000. This is a safeguard to prevent incorrect API calls.
* Varsome annotations are stored locally and will not be fetched again unless the local file is deleted.
* ``copy`` parameter to :meth:`~assay._Assay.get_attribute` to return a view of the data instead of a copy.
* Option to pass ``order`` of labels to :meth:`~assay._Assay.ridgeplot`.
* ADO score is formatted more conveniently in the :class:`workflows.variant_subclone_table.VariantSubcloneTable` workflow. If it's 0, then it's shown as "-" and if <0.05 then it's shown as "~0.0".
* Ability to rename a sample using :meth:`~sample.Sample.rename`.


Changed
~~~~~~~

* :attr:`sample.Sample.name` is a now a property, and cannot be set. It returns a value according to the current ``sample_name`` metadata.
* :attr:`assay._Assay.title` is a now a property, and cannot be set. It returns a value according to the current `sample_name` metadata.
* Behavior of ``default_label`` in :meth:`assay._Assay.set_labels`. When ``default_label`` is ``None``, only the labels of the provided barcodes are updated.
* ``normalized_counts`` in :meth:`~cnv.Cnv.compute_ploidy` is no longer used. The ``read_counts`` layer is used directly.
* ``ANNOTATION_COLUMNS`` constant was moved to  ``missionbio.annotation.constants``
* Use ``pynndescent`` instead of ``scikit-learn`` to speed up nearest neighbors calculation during graph-community clustering. Results will not be backwards compatible.

Fixed
~~~~~

* Ordering of the barcodes in the heatmap when a subset of the variants are used.
* Fetching of CNV amplicon gene names for regions where ensembl returns an incomplete response.
* Allow custom grouping of amplicons for :meth:`cnv.CNV.heatmap` by passing amplicons to ``features`` and ``x_groups`` values.


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
