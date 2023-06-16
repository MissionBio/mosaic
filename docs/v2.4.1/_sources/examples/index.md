---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: '0.8'
    jupytext_version: '1.4.2'
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Code Snippets

## Annotate your variants

This example shows how you can annotate your variants. Running the command below will output a pandas dataframe.

```{code-cell} ipython3
---
render:
  image:
    width: 200px
---
import missionbio.mosaic as ms
sample = ms.load_example_dataset("3 cell mix")
filtered_variants = list(sample.dna.filter_variants())

sample.dna.get_annotations(filtered_variants[0:5])
```

Currently we provide the following annotations:

* Variant type
* Gene
* Gene function
* RefSeq transcript ID
* cDNA change
* Protein change
* Protein coding impact
* COSMIC
* DANN SNVs
* ClinVar
* gnomAD
* dbSNP

If you need additional annotation sources, please contact us.


## Multi-assay heatmap

The following examples demonstrate how to produce a heatmap showing data from multiple assays. The first example shows how to cluster cells by protein expression, then produce a heatmap that shows the per-cluster protein expression and DNA mutation status for some select variants.

```{code-cell} ipython3
:tags: [remove-stdout,remove-stderr]

import missionbio.mosaic as ms

sample = ms.load_example_dataset("3 cell mix")

# first, cluster by protein expression
sample.protein.normalize_reads()
sample.protein.run_pca(attribute='normalized_counts', components=5)
sample.protein.run_umap(attribute='pca')
sample.protein.cluster(attribute='pca', method='graph-community', k=100)

# show only two DNA variants
sample.dna = sample.dna[:, filtered_variants[0:2]]

sample.heatmap(
    clusterby='protein',
    sortby='dna',
    drop='cnv',
    flatten=False
)
```

If you cluster by protein, you can also quantify the percentage and mutated cells in each cluster for your mutation(s) of choice.

```{code-cell} ipython3
:tags: [remove-stdout,remove-stderr]

import missionbio.mosaic as ms

sample = ms.load_example_dataset("3 cell mix")

# first, cluster by protein expression
sample.protein.normalize_reads()
sample.protein.run_pca(attribute='normalized_counts', components=5)
sample.protein.run_umap(attribute='pca')
sample.protein.cluster(attribute='pca', method='graph-community', k=100)

# show only two DNA variants
sample.dna = sample.dna[:, filtered_variants[0:2]]

sample.heatmap(
    clusterby='protein',
    sortby='dna',
    drop='cnv',
    flatten=True,
    quantify_dna_mut=True
)
```

## Fishplot to visualize clonal evolution

Draws a fish plot and associated graphical representation of clonal phylogeny. Currently, you must provide the phylogenetic relationships between clones.

```{code-cell} ipython3
:tags: [remove-stdout,remove-stderr]

import missionbio.mosaic as ms

group = ms.load_example_dataset('Multisample PBMC')
group.fishplot(labels=["Clone 1", "Clone 2"], parents=[None, None])
```

## Group cells by a select number of DNA variants

Clusters cells into clones based on the provided variants and returns a dataframe of per-clone and per-variant statistics. This algorithm also takes into consideration allele dropout out (ADO) to identify potential false positive clones.

```{code-cell} ipython3
:tags: [remove-stdout,remove-stderr]

import missionbio.mosaic as ms

sample = ms.load_example_dataset('3 cell mix')
filtered_variants = sample.dna.filter_variants()
sample.dna.group_by_genotype(features=filtered_variants[0:5])
```