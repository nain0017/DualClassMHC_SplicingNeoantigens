# Reference resources: versions and provenance

All references were fetched fresh at the start of the pipeline lock (23 May 2026) and pinned for the duration of the analysis.

## Genome

**GRCh38 plus ERCC controls plus SIRV controls** (Monorail-external distribution, as used by recount3).

- Source: <https://recount-opendata.s3.amazonaws.com/recount3/release/human/annotations/gene_sums/monorail_external/human.gene_sums.G026.gz>
- Rationale for Monorail-external index (rather than plain GRCh38): matches the recount3 processing pipeline exactly, enabling direct comparison of downstream junction and expression outputs with published recount3-derived resources.

## Alignment annotation (GENCODE v26)

**GENCODE v26 comprehensive annotation** (matches the Monorail alignment index).

- Source: <ftp://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_human/release_26/gencode.v26.annotation.gtf.gz>
- Used for STAR alignment `--sjdbGTFfile` parameter and for regtools junction annotation overlap in Stage A2.

## Peptide translation annotation (GENCODE v45)

**GENCODE v45** (used only downstream of alignment, for peptide translation and modified-protein output).

- Annotation source: <ftp://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_human/release_45/gencode.v45.annotation.gtf.gz>
- Protein FASTA source: <ftp://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_human/release_45/gencode.v45.pc_translations.fa.gz>
- Rationale for the v26 or v45 split: alignment index construction is expensive and version-locked to Monorail-external; peptide-level annotation benefits from the newer v45 canonical proteome (45,892 proteins), which better represents recent transcript refinements.

## HLA database

**IMGTHLA release 3.43.0** (used by arcasHLA for HLA typing).

- Source: <https://github.com/ANHIG/IMGTHLA/tree/3430>
- Installed via `arcasHLA reference --version 3.43.0`.

## Published resources

- **Patterson and Auslander 2022 neoantigen resource:** Zenodo record [6998939](https://zenodo.org/records/6998939). Provides the published mutation-derived neoantigen load and per-sample TMB used in orthogonality analyses (Hugo and Riaz cohorts).

- **SpliceMutr** (Palmer et al. 2024, Cancer Res Commun 4:3137-3150): DOI [10.1158/2767-9764.CRC-23-0309](https://doi.org/10.1158/2767-9764.CRC-23-0309). The SA score formula adapted here is derived from the SpliceMutr framework with three documented deviations locked in pre-registered amendment v5.4.12.

## Verification

Each reference file was verified by MD5 sum at download time and archived at Zenodo alongside the intermediate pipeline outputs. See the Zenodo DOI (to be added upon submission) for the full manifest.
