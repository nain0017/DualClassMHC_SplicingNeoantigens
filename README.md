# Splicing-derived dual-class MHC neoantigens in melanoma anti-PD-1 response

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21347505.svg)](https://doi.org/10.5281/zenodo.21347505)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Pre-registered three-cohort analysis of RNA-splicing-derived MHC class I and class II neoantigens in melanoma patients treated with anti-PD-1 immunotherapy.

**Author:** MD. Zulkarnain Sajid
**ORCID:** [0009-0002-6874-0497](https://orcid.org/0009-0002-6874-0497)
**Correspondence:** zulkarnainsajid4768@gmail.com

## Summary

This repository contains the complete analysis pipeline and pre-registration record for a study that identifies 20 splicing-derived dual-class MHC neoantigen cluster-tuples (mapping to 21 named genes) that are consistently produced across three published melanoma anti-PD-1 cohorts (Hugo 2016, Riaz 2017, Gide 2019; n=92 evaluable patients). Two orthogonality findings show that the resulting per-sample splicing antigenicity score is distinct from tumor mutational burden and from published mutation-derived neoantigen load. A cohort-specific survival association in Gide 2019 is internally robust across overall survival (HR=2.61, 95 percent CI 1.56 to 4.38, p=0.0003) and progression-free survival (HR=1.80, 1.17 to 2.77, p=0.0075) endpoints, though it did not replicate cross-cohort at the current sample size.

## Repository structure

```
DualClassMHC_SplicingNeoantigens/
├── README.md                       This file
├── LICENSE                         MIT
├── requirements.txt                Python package pins
├── environment.yaml                Conda environment
├── reference_versions.md           Genome and annotation versions
├── notebooks/
│   └── pipeline.ipynb      Complete pipeline (Colab-native)
├── src/                           Modular pipeline scripts (see README in dir)
├── pre_commitments/               Dated amendment records (v1 to v5.4.16)
├── supplementary_tables/          Supplementary Tables T1 to T10 (CSV)
├── figures/                       Main and supplementary figures (PNG)
├── environment/                   Pipeline environment notes
│   └── phase_g_v52_env_record.json 12 documented pipeline gotchas
└── figures/                       Main and supplementary figures (PNG)
```

## Reproducibility

### Software environment

The complete pipeline was executed on Google Colab (T4 GPU runtime, high-RAM). Software versions are pinned in `requirements.txt` (pip) and `environment.yaml` (conda). Key tools:

- **STAR 2.7.3a** for RNA-seq alignment (Monorail-canonical parameters)
- **samtools 1.9** for BAM sorting and indexing
- **regtools 1.0.0** for junction extraction
- **arcasHLA 0.5.0** with Kallisto 0.44.0 and IMGTHLA database v3.43.0 for HLA typing
- **LeafCutter-DS** Python and pyro re-implementation for differential intron usage (see [pre_commitments/amendment_v5.4.3.md](pre_commitments/amendment_v5.4.3.md) for the substitution rationale)
- **MHCnuggets 2.4.0** with source patches for Keras 3 compatibility, for MHC binding prediction
- **lifelines 0.27.10** for survival analysis
- **scipy 1.13**, **statsmodels 0.14** for statistical tests
- **gseapy 1.1.3** for pathway enrichment via the Enrichr API

Reference resources:
- **GRCh38** genome plus ERCC plus SIRV controls via the Monorail-external index (recount3 distribution)
- **GENCODE v26** annotation for alignment (matches the alignment index)
- **GENCODE v45** annotation for peptide translation and modified-protein output

### Data availability

Raw RNA-seq data for the three cohorts are available at the primary sources:
- Hugo 2016: SRA project **SRP070710** (26 patients used)
- Riaz 2017: SRA project **SRP094781** (32 patients used)
- Gide 2019: ENA project **PRJEB23709** (34 patients used)

Processed intermediate outputs (STAR alignments, junction BEDs, arcasHLA JSON, MHCnuggets binder tables) are too large for GitHub and are archived separately at Zenodo (DOI to be added upon submission).

Small analysis outputs (final cluster-tuple tables, per-sample SA scores, orthogonality inputs, survival Cox outputs) are in `supplementary_tables/` as Supplementary Tables T1 to T10.

## Pre-registration

All primary outcome thresholds were pre-committed in writing before observation in a dated amendment sequence. See `pre_commitments/` for the full record and `pre_commitments/README.md` for a summary.

The essential pre-committed thresholds:

- **Discovery outcome (a):** at least 20 cluster-tuples meeting the dual-class binder criterion (class I 9-mer IC50 less than 500 nM AND class II 15-mer IC50 less than 1000 nM in the same cluster-tuple). **Result: met (20 of 20 threshold, met exactly).**
- **Discovery outcome (b):** splicing-derived neoantigen burden differential between R and NR at cross-cohort Stouffer p less than 0.05. **Result: not met.**
- **Discovery outcome (c):** Tier 3 high-confidence subset recovering at least 8 of 32 cluster-tuples in the dual-class binder set. **Result: partial (2 of 32; B4GALT7 and IRAK4).**
- **Response outcome:** cross-cohort Stouffer p less than 0.05 for the per-sample SA score. **Result: not met (min p = 0.122 for SA class II).**
- **Survival outcome:** cross-cohort Cox HR greater than 1.5 with p less than 0.05 for at least one SA metric. **Result: not met cross-cohort; met specifically in Gide (SA class II OS HR=2.61, p=0.0003).**
- **Orthogonality outcome:** absolute Spearman rho less than 0.3 across all cohorts for SA versus TMB and SA versus published mutation-derived neoantigen load. **Result: met (max absolute rho = 0.225 versus TMB, 0.102 versus published neoantigen load).**


## Citation

If you use this pipeline or the pre-registration framework, please cite:

> Sajid MZ. Splicing-derived dual-class MHC neoantigens in melanoma anti-PD-1 response: a pre-registered three-cohort analysis. (In preparation.)

Software release (this repository):

> Sajid MZ. DualClassMHC_SplicingNeoantigens (v1.0.0). Zenodo. [https://doi.org/10.5281/zenodo.21347505](https://doi.org/10.5281/zenodo.21347505)

## License

MIT License. See [LICENSE](LICENSE) for details.

## Acknowledgments

I thank the authors of the Hugo 2016, Riaz 2017, and Gide 2019 cohorts for making raw data publicly available, and the authors of LeafCutter (Li et al. 2018), MHCnuggets (Shao et al. 2020), arcasHLA (Orenbuch et al. 2020), recount3 (Wilks et al. 2021), SpliceMutr (Palmer et al. 2024), and the Patterson and Auslander 2022 neoantigen resource for making their tools and derived data publicly available. I also thank Prof. Tapati Basak (Jahangirnagar University) for advisor input during early stages of my thesis work.
