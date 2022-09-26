.. _getting_started:

Getting Started
===============

Loading a sample
----------------
1. First import missionbio.mosaic and define your h5path, or path to your h5 file on your local device:
    .. code-block::

        import missionbio.mosaic as ms
        h5path = '/Users/botero/Desktop/Sample data/4-cell-lines-AML-multiomics/4-cell-lines-AML-multiomics.dna+protein.h5'
2. Load in your h5 file:
    .. code-block::

        sample = ms.load(h5path, raw=False, apply_filter=True, single=True)

    - The first variable in your load function is the h5path which is defined above.
    - Next is the raw variable, which is set to False in most cases. Changing this to True will load in all barcodes and raw counts.
    - The apply_filter variable is generally set to True, which will only load in filtered dna variants. In some cases your variants of interest may not meet filter criteria, in which case you can change this to False, to load in all dna variants.
    - The single variable is set to False by default and will load in merged h5s as separate samples. **In the current version of Mosaic**, many graphs are built around this being set to True to load in merged h5s in as a single sample. However, if you wish to make a Fishplot (shown in Multisample analysis: Multisample plots, or Code Snippets: Fishplot to visualize clonal evolution), or run analysis shown in Multisample analysis, you will still need to set this to False.
    - Note you can also add a whitelist to this load function to ensure that variants of interest are included, despite filtering thresholds. See the example below:
        .. code-block::

            sample = ms.load(h5path, raw=False, apply_filter=True, single=True whitelist = ["chr1:115258747:C/T", "chr2:198266834:T/C", "chrX:133547940:C/T"])
3. Once the analysis is complete, it can be saved using:
    .. code-block::

        mio.save(sample,'/path/to/save/h5')
Merging h5 files
----------------
Multiple h5 files can be merged into one h5 file prior to loading into Mosaic. This code should be run in a terminal/console. Note, this can also be done on the Tapestri pipeline, but this may be the preferred method if you are merging pre-filtered h5 files.

1. Activate your anaconda environment
    .. code-block::

        > conda activate mosaic

2. Call tapestri h5 merge -h to show all all of the different calls you can make with this command.
    .. code-block::

        > tapestri h5 merge -h

3. To merge files, run this command tapestri h5 merge samples followed by the files you want to merge, and lastly the name for the new output file.
    .. code-block::

        > tapestri h5 merge samples sample1.h5 sample2.h5 sample3.h5 merged.h5



Tutorials
---------

The best way to learn Mosaic is through our Jupyter notebook :ref:`all-vignettes`,
which demonstrate basic tutorials on how to use Mosaic to analyse
DNA + Protein data.

