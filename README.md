# Reusable immunofluorescence analysis

Open `05_reusable_immunofluorescence_quantification.ipynb` in Jupyter or VS Code.

## Inputs
CellProfiler `Image.csv`, `Nuclei.csv`, `Cells.csv`, `Cytoplasm.csv` and a plate-map CSV containing `Well` and `Treatment`. Select the experiment folder with the dialog (or set `DATA_DIR` explicitly). If a plate map cannot be uniquely identified, select it in the file dialog.

## Reuse
Change `ANTIBODY_PANEL` and `EXPERIMENT_ID` for each independent experiment. By default, all detected intensity, area and puncta-count features are analyzed. Restrict `FEATURES_BY_COMPARTMENT` when only selected channels are relevant. No fixed LC3/MTMR4 feature names are required.

## Calculations
Objects are matched to images via `ImageNumber`, then object-level values are averaged by `Well` and `Treatment`. Each compartment's features are normalized to the experiment's `Non_Treatment` wells with `(x - mean(control))/std(control, ddof=0)`, matching the intended Excel `STDEV.P` procedure.

## Outputs
`immunofluorescence_results/<ANTIBODY_PANEL>/<EXPERIMENT_ID>/` contains one workbook with mean, Z-score, and reference parameter sheets plus CSV tables.

## Limitations and checks
Not yet executed on the original CellProfiler CSV exports, which were not supplied. The image well is extracted from `FileName_GFP` if `Well` is absent, matching the original notebook; adjust this for experiments without GFP. This version avoids merging image measurement columns into object measurements and therefore does not use the original `_x` column suffixes. Verify that the selected raw feature columns match those used in each original experiment. Run separately for each biological experiment. Excel reference was supplied for one cell table only; full end-to-end numerical equivalence cannot yet be confirmed. Requires pandas, numpy, matplotlib, openpyxl and a local Python GUI for dialogs.
