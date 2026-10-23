# Nanoparticle–Cell Interactions: Image Analysis and Protein Corona Characterization

## Overview

This repository contains Jupyter notebooks developed for the analysis of nanoparticle–cell interactions, high-content microscopy data, protein corona characterization, and hyperspectral imaging.

The analytical workflows combine image-derived morphological features, single-cell profiling, statistical analysis, machine learning, proteomics, and physicochemical characterization of gold nanoparticles (AuNPs).

The notebooks are organized into nine modules, covering data processing, feature extraction, classification, statistical analysis, and visualization.
## Computational Environment and Installation

All analyses were performed using Python within a dedicated Conda environment named `aunp_analysis`.

The complete environment configuration, including package dependencies and versions, is provided in the `environment.yml` file.

### Installation

To recreate the environment, clone this repository and execute:

```bash
conda env create -f environment.yml
conda activate aunp_analysis
```

### Running the Notebooks

Open JupyterLab:

```bash
jupyter lab
```

Select the `aunp_analysis` Python environment as the notebook kernel.

**Note:** Some dependencies may require platform-specific adjustments.

## Repository Structure

### 01 — Single-Cell SQLite Retrieval

**Notebook:** `01_single_cell_sqlite_retrieval.ipynb`

Retrieves and organizes single-cell measurements from SQLite databases generated during microscopy image analysis.

**Main objectives:**
- Import cell-level measurements from SQLite databases.
- Retrieve measurements associated with different cellular compartments.
- Organize morphological, intensity, texture, and other image-derived features.
- Prepare structured datasets for downstream analyses.

### 02 — Well Aggregation, Annotation, and Normalization

**Notebook:** `02_well_aggregation_annotation_normalization.ipynb`

Processes single-cell measurements to generate annotated and normalized datasets suitable for statistical analysis and phenotypic profiling.

**Main objectives:**
- Aggregate single-cell measurements at the well level.
- Associate measurements with experimental metadata.
- Organize samples according to treatments and experimental conditions.
- Normalize quantitative features for downstream comparisons.

### 03 — LDA and K-Means Classification

**Notebook:** `03_lda_kmeans_classification.ipynb`

Applies multivariate statistical methods and unsupervised machine learning to investigate phenotypic differences between experimental groups.

**Main objectives:**
- Explore high-dimensional cellular profiling data.
- Apply Linear Discriminant Analysis (LDA) to evaluate group separation.
- Use K-means clustering to identify patterns within the dataset.
- Visualize phenotypic relationships between experimental conditions.

### 04 — Morphological Feature Statistics

**Notebook:** `04_morphological_feature_statistics.ipynb`

Performs statistical comparisons of morphological and image-derived cellular features across experimental conditions.

**Main objectives:**
- Analyze quantitative morphological measurements.
- Compare feature distributions between treatments.
- Identify features associated with cellular phenotypic changes.
- Generate statistical summaries and publication-oriented visualizations.

### 05 — Reusable Immunofluorescence Quantification

**Notebook:** `05_reusable_immunofluorescence_quantification.ipynb`

Provides a reusable workflow for quantitative analysis of immunofluorescence microscopy measurements.

**Main objectives:**
- Organize fluorescence intensity measurements.
- Quantify marker-associated cellular responses.
- Compare experimental groups.
- Generate graphical and statistical summaries of immunofluorescence data.

### 06 — CPS Protein Corona Thickness Estimation

**Notebook:** `06_cps_protein_corona_thickness_estimation.ipynb`

Investigates protein corona thickness using centrifugal particle sedimentation (CPS), also known as differential centrifugal sedimentation (DCS), measurements.

Protein adsorption can alter both the physical diameter and effective density of nanoparticles, influencing their sedimentation behavior.

**Main objectives:**
- Analyze CPS-derived apparent particle diameters.
- Apply a core–shell model to investigate nanoparticle–protein complexes.
- Estimate physical particle diameter and corona thickness under defined density assumptions.
- Examine how changes in effective density influence sedimentation-based measurements.

**Important consideration:** Corona thickness estimates depend on the assumptions used for particle geometry, core size, shell density, medium density, and instrument settings. CPS-derived diameters should not be interpreted directly as physical corona thickness.

### 07 — AuNP Protein Corona Proteomics

**Notebook:** `07_aunp_protein_corona_proteomics (2).ipynb`

Supports the analysis of protein composition associated with gold nanoparticles following exposure to biological fluids.

**Main objectives:**
- Organize protein identification and abundance datasets.
- Compare protein corona compositions across experimental conditions.
- Investigate differences in protein enrichment and relative abundance.
- Support biological interpretation of nanoparticle protein corona composition.

### 08 — Gold Pixel Reference Spectral Library

**Notebook:** `08_gold_pixel_reference_spectral_library.ipynb`

Processes reference hyperspectral spectra to characterize spectral signatures associated with gold nanoparticles.

**Main objectives:**
- Import reference spectral library data.
- Identify peak wavelengths from individual reference spectra.
- Organize spectral identifiers and corresponding peak wavelengths.
- Generate a reference table for subsequent hyperspectral image analysis.

**Key output:**

`reference_library_peak_wavelengths.csv`

This reference table provides the spectral information used in Notebook 09.

### 09 — AuNP Hyperspectral Distribution

**Notebook:** `09_aunp_spectral_distribution.ipynb`

Analyzes hyperspectral image classification reports to investigate the distribution of gold nanoparticle-associated spectral signatures across experimental conditions.

The workflow combines classified pixel counts with peak wavelengths obtained from the reference spectral library.

**Main objectives:**
- Read CytoViva classification reports, including text files without extensions.
- Identify experimental groups from image filenames.
- Match classified spectral regions with the corresponding reference spectra.
- Apply quality-control criteria based on the number of classified regions.
- Exclude files with inconsistent region counts relative to their group.
- Quantify the distribution of classified pixels across peak wavelengths.
- Aggregate spectral distributions by experimental condition.
- Generate graphical representations, including violin plots and wavelength distribution plots.

**Key outputs include:**

- `image_classification_qc_all_files.csv`
- `image_peak_wavelength_counts_labeled.csv`
- `group_peak_wavelength_counts_long.csv`
- `peak_wavelength_counts_by_group.csv`
- `peak_wavelength_observations_by_group.csv`

The analysis provides a framework for investigating changes in hyperspectral signatures associated with different nanoparticle treatments.

## General Analysis Workflow

The repository contains complementary analytical modules rather than a single mandatory sequential pipeline.

**Cellular image analysis:**

```text
Microscopy measurements
         |
         v
01 — Single-cell data retrieval
         |
         v
02 — Well aggregation and normalization
         |
         +----------------------------+
         |                            |
         v                            v
03 — LDA / K-means         04 — Morphological statistics
         |
         v
Phenotypic characterization
```

**Complementary characterization:**

```text
05 — Immunofluorescence quantification

06 — CPS / protein corona thickness estimation

07 — Protein corona proteomics
```

**Hyperspectral analysis:**

```text
Reference spectral library
         |
         v
08 — Peak wavelength extraction
         |
         v
Reference peak wavelength table
         |
         +---- CytoViva classification reports
                         |
                         v
              09 — Spectral distribution
                         |
                         v
             QC, aggregation and plots
```

## Computational Environment

The notebooks are designed for execution in Python-based Jupyter environments.

Depending on the analytical workflow, commonly used libraries include:

- `pandas` — Data manipulation and organization
- `numpy` — Numerical computation
- `matplotlib` — Scientific visualization
- `seaborn` — Statistical visualization
- `scipy` — Scientific and statistical calculations
- `scikit-learn` — Machine learning and multivariate analysis
- `statsmodels` — Statistical analysis and multiple-comparison procedures

Package requirements may vary between notebooks.

## Data Availability and Reproducibility

Some workflows require experimental data generated using microscopy, hyperspectral imaging, CPS/DCS, or mass spectrometry.

Raw experimental datasets may not be included in this repository because of file size, storage requirements, or data-sharing restrictions.

Users should configure local input and output directories before executing the notebooks.

The analyses should be interpreted according to the experimental design, including the distinction between biological replicates, technical replicates, single-cell measurements, and individual classified pixels.

## Research Applications

These computational workflows support research into:

- Gold nanoparticle–cell interactions
- Biomolecular and protein corona formation
- Nanoparticle physicochemical characterization
- High-content cellular phenotyping
- Quantitative immunofluorescence
- Proteomic characterization
- Hyperspectral microscopy
- Multivariate statistical analysis

## Author

**Luana Pereira Cardoso**

PhD Researcher  
University of Campinas (UNICAMP), Brazil

## Citation

If you use or adapt these workflows in scientific research, please acknowledge this repository and cite the associated scientific publications when available.
