# Brain Atlas Resolution & Dimensionality Reduction — Sex Classification from Gray Matter Density

BMDE 520, McGill University — Challenge 3.

Predicts subject sex from voxel-based morphometry (VBM) gray-matter density
maps (OASIS-1, 100 subjects via `nilearn`'s `fetch_oasis_vbm`), and studies how
the choice of brain atlas and dimensionality-reduction method affects
classification accuracy.

## What's here

- **Atlas-resolution sweep**: ROI-averaged features extracted with
  `NiftiLabelsMasker` across the Schaefer 2018 and Craddock 2012/2011 atlases
  at multiple parcellation resolutions (100–1000 regions), each evaluated with
  logistic regression.
- **Dimensionality-reduction comparison** at the best-performing atlas
  resolution: PCA, K-means (as a feature transform), and univariate
  `SelectKBest` feature selection, each swept across a range of
  components/clusters/features to find the accuracy-vs-dimensionality curve.
- **Multi-resolution stacking**: an ensemble that stacks logistic-regression
  predictions trained at each atlas resolution into a meta-classifier.
- **Best-atlas selection**: automatically picks the Craddock parcellation
  variant with the most regions and reruns the PCA/K-means/SelectKBest sweeps
  on it specifically.

## Files

- `challenge3_andrea_gomez.ipynb` — full notebook: data loading, feature
  extraction, atlas sweep, dimensionality-reduction comparisons, and stacking.

## Data (not included)

This notebook uses two datasets that are **not** included in this repo:

- **OASIS-1** gray-matter maps, fetched via
  `nilearn.datasets.fetch_oasis_vbm(n_subjects=100)`. OASIS data is distributed
  under its own [data usage agreement](https://sites.wustl.edu/oasisbrains/) —
  `nilearn` handles the download once you accept it.
- **Craddock 2011/2012 atlas parcellations** — the notebook works around
  `nilearn`'s `fetch_atlas_craddock_2012` by pointing directly at a local
  `craddock_2011_parcellations/` folder of NIfTI files; download the atlas
  separately and update the path in the notebook to match where you saved it.

## Author

Andrea Paola Gómez Jaime
