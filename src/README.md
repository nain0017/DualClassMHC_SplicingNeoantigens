# Source pipeline modules

This directory is scaffolded for optional modular refactoring of the pipeline. The primary reference implementation is the Colab notebook at `../notebooks/pipeline.ipynb`, which contains all 240 cells that produced the manuscript results.

## Two ways to reproduce

### Path 1: Notebook (canonical)

Open `../notebooks/pipeline.ipynb` in Google Colab with a T4 GPU high-RAM runtime. The notebook is self-contained and calls out to the software pinned in `../environment.yaml` and `../requirements.txt`. All 240 cells execute in order and produce the outputs archived under Supplementary Tables T1 to T10.

### Path 2: Modular scripts (planned)

For readers who prefer script-based reproduction, this directory will contain modular Python scripts by pipeline stage. Modules are planned as:

- `01_cohort_assembly.py` — Sample list construction and response label harmonization for Hugo, Riaz, Gide
- `02_alignment.py` — STAR alignment orchestration with Monorail-canonical parameters
- `03_leafcutter_ds.py` — LeafCutter-DS Python re-implementation (Dirichlet-multinomial GLM with pyro inference)
- `04_meta_analysis.py` — Signed Stouffer combine with sample-size weights
- `05_junction_mapping.py` — Junction-to-transcript mapping with plus 9 / minus 9 coordinate offset
- `06_modified_proteins.py` — Modified protein sequence generation from significant cluster-tuples
- `07_mhc_binder_prediction.py` — MHCnuggets class I and class II binder prediction
- `08_sa_score.py` — SpliceMutr-adapted SA score per sample
- `09_response_survival.py` — Response Stouffer analysis, Cox univariate survival, Kaplan-Meier plots
- `10_orthogonality.py` — SA versus TMB and SA versus published neoantigen load Spearman rho with Fisher z-combine
- `11_pathway_enrichment.py` — Enrichr API pathway enrichment
- `patch_mhcnuggets.py` — Automated Keras 3 patch (see `../environment/mhcnuggets_keras3_patch.md`)

Extraction from the notebook is planned as a follow-up task. Priority order matches the module numbering.

## Reference implementations of substituted tools

### LeafCutter-DS

The Python re-implementation of the LeafCutter differential intron usage test lives under `leafcutter_ds/` (to be extracted). The mathematics is unchanged: per-cluster Dirichlet-multinomial GLM comparing case versus control, with a likelihood-ratio test for null (all coefficients equal) versus alternative (case-vs-control effect estimated). Inference uses pyro variational inference rather than Stan Hamiltonian Monte Carlo. Convergence and coverage were validated against a subset of the LeafCutter-published melanoma differential-splicing hits from Li et al. 2018.

### Mann-Whitney U orthogonal validation

The Mann-Whitney U substitute for Bisbee lives under `mw_u_orthogonal/` (to be extracted). Per-cohort, per-cluster Mann-Whitney U between R and NR patients on splicing quantifications, with per-cohort concordance thresholded at 80 percent as originally pre-registered for Bisbee.
