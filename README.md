# Live Cell Painting — curated notebook review

This folder contains **four individually reorganized Jupyter notebooks** for the rat-serum AuNP Live Cell Painting analysis. Every notebook has experiment-specific English Markdown describing the actual processing steps. Original files are retained under `originals/`.

## Recommended order

1. `01_single_cell_sqlite_retrieval.ipynb` — read three CellProfiler SQLite plates and export single-cell measurements.
2. `02_well_aggregation_annotation_normalization.ipynb` — count nuclei-associated rows, aggregate by well (median), annotate platemaps, normalize each plate to negative controls (`mad_robustize`), and select features.
3. `03_lda_kmeans_classification.ipynb` — standardized LDA, plots, three-cluster K-means in LDA1/LDA2 space, cluster–class contingency matrix, top 30 features.
4. `04_morphological_feature_statistics.ipynb` — individual-feature ANOVA/Tukey and all confirmed category-level Welch-test summaries (measurement type, cellular compartment, and fluorescence channel).

## Before execution

- Supply the original CellProfiler SQLite databases, plate barcode/platemap metadata, and the Broad Institute `scripts_notebooks_fossa` dependency. The source is https://github.com/broadinstitute/scripts_notebooks_fossa; pin the Git commit for reproducibility and follow its license.
- Change the `DATABASE_ROOT`, `SCRIPTS_PARENT`, and `INPUT_CSV` settings where marked. Notebook 02 retains the original interactive `profiling_inputs()` helper.
- Install packages: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `scikit-learn`, `statsmodels`, `pycytominer` and upstream helper dependencies.
- **These notebooks have been syntax-checked, but have not been run on the original experimental data.** Exact numeric equivalence to the original results has not yet been verified.


