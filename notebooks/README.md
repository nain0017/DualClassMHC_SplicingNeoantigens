# Pipeline notebook

## `pipeline.ipynb`

The complete pipeline that produced the manuscript results. Organized into 13 sequential stages with markdown section headers.

- **93 code cells** (down from 240 in the raw working notebook, plus 2 essential cells restored from a companion data-processing notebook)
- **15 markdown cells** — title, 13 stage headers, footer
- **1.05 MB** file size (down from 19.7 MB)
- **All cell outputs stripped** — the notebook needs to be re-executed in Colab to produce outputs
- **All formatting-only comments stripped** — `# ==========` separators, `# CELL L2-XXX` cell labels, empty comment lines, and redundant blank lines removed (~980 lines of noise). Substantive comments explaining code intent, methodology, and pre-registration reasoning are preserved.

## Cells integrated from a companion notebook

Two cells that were essential for re-runnability were originally in a separate data-processing notebook. They have been merged into this pipeline notebook at the correct pipeline stages:

- **Cell M-fix (Riaz manifest PRE-treatment filter)** — placed at the end of Stage 1. Filters the 109-row Riaz manifest down to anti-PD-1 PRE monotherapy biopsies (~49 samples per Charter v5). Backs up the unfiltered version before overwriting.
- **Cell C-Hugo (Hugo STAR alignment)** — placed at the end of Stage 2 alongside the Gide alignment. Uses the same v5.2 pipeline as Gide (STAR sorted BAM + GeneCounts + samtools index + regtools + arcasHLA extract + genotype). Runs in resumable batches of 12 samples; re-execute until all Hugo samples complete.

## Re-runnability

**This notebook is now runnable end-to-end from raw data**, provided the prerequisites below are in place. Both the Hugo and Gide alignment cells have been integrated:

- **Stage 1 end** — Riaz manifest filter (Cell M-fix) filters to anti-PD-1 PRE monotherapy biopsies
- **Stage 2** — includes `%%writefile gide_batch_align.py`, a Gide alignment wrapper cell (invokes the utility on all 41 samples with `--skip_completed`), and Cell C-Hugo which STAR-aligns the Hugo cohort using the same v5.2 pipeline

Riaz raw data is loaded via `recount3_loader.R v4` with the filtered manifest (already in Stage 1). If you prefer to STAR-align Riaz from raw fastqs (matching the Hugo/Gide path), you will need to add a Cell C-Riaz cell to Stage 2 following the same pattern as Cell C-Hugo — this cell is not currently in either shared notebook.

## What was removed during curation

The raw working notebook contained 240 cells accumulated during development. Removed:

- **Phase 1 cohort exploration** (~30 cells): Auslander 2018 (dropped per amendment v5 for annotation reproducibility concerns), Du 2021 (rejected per v5 for incompatible RNA-seq protocol), Snaptron REST fallback (unused), archive-vs-keep decisions
- **Test and retest cells** (~60 cells): initial pipeline validations that were superseded by the FIX / V2 / V3 final versions
- **Diagnostic and inspection cells** (~40 cells): `df.head()`, `df.shape`, directory listings, quick verifications
- **Salmon exploration** (~5 cells): Salmon was dropped at amendment v5.2 in favor of the STAR SJ.out.tab and regtools path
- **Duplicate `pip install`** cells
- **Session restore and recovery cells** after Colab disconnects
- **Batch launch retries** for Gide alignment: kept one representative launch cell and the final audit

## Pipeline stage structure

| Stage | Content | Key amendments |
|-------|---------|---------------|
| 0 | Environment setup and Drive mount | |
| 1 | Cohort assembly utilities (R scripts) | |
| 2 | STAR alignment (Gide batch) | v5.1 |
| 3 | Environment finalization + Phase G validation | v5.2 |
| 4 | Clinical response label harmonization | v5.4.1, v5.4.2 |
| 5 | LeafCutter-DS setup + Hugo differential splicing | v5.4.3, v5.4.4 |
| 6 | Riaz + Gide differential splicing + Stouffer meta | v5.4.5, v5.4.5-R, v5.4.6 |
| 7 | Bisbee substitution + paradigm re-scope | v5.4.7, v5.4.8, v5.4.9, v5.4.10, v5.4.11 |
| 8 | Peptide pipeline (SpliceMutr-adapted) | v5.4.12 |
| 9 | SA score + cross-cohort response | v5.4.13 |
| 10 | Survival + TMB orthogonality | v5.4.14 |
| 11 | Secondary analyses (SF mutations, neoAg load, PFS, GO, Tier 3) | |
| 12 | Figure generation (F1-F5, S1-S5) | |

## Sensitivity analyses (Path Y)

Both pre-registered sensitivity analyses (Charter v5.4.15 Hugo purity, v5.4.16 class II 500 nM) are integrated into Stage 12 of the notebook. Both were executed on 18 June 2026 with verified results matching the manuscript claims:

- **Y1-FIX-v2 (v5.4.15):** verdict `stable_under_purity_normalization`. Hugo tumor purity 26/26 samples, median 0.590. Riaz and Gide disclosed as data-availability limitations. Direction and significance stable under purity normalization.
- **Y2-FIX (v5.4.16):** verdict `robust_to_threshold`. All 20 of 20 dual-class cluster-tuples retained under the tightened class II IC50 500 nM threshold. All 21 gene symbols preserved. Zero cluster-tuples lost.

Both cells save output to `stage2_outputs/_story_a/path_y/` in the Drive project directory.

## What you may need to add or verify

1. **Sensitivity analysis cells (v5.4.15, v5.4.16)** — see the KNOWN GAPS section above
2. **In-notebook data outputs** — the notebook was stripped of all outputs during curation; re-executing in Colab is required to produce Supplementary Tables T1 through T10 in `../supplementary_tables/`
3. **Charter amendment display cells** — the `# Save Charter v5.4.X amendment` cells write amendment JSON to Drive; if you want these amendments to also render as markdown documentation IN the notebook, they can be moved to markdown cells with a small refactor
4. **Verify no debug `print()` statements remain inside kept cells** — the curation removed whole cells that were pure debug, but individual `print()` statements inside pipeline cells were preserved as-is because some are informational logging (which is fine)

## Reproduction

To reproduce the pipeline:

1. Open this notebook in Google Colab
2. Set runtime to T4 GPU with high-RAM enabled
3. Ensure your Google Drive is mounted at `/content/drive/MyDrive/DualClassMHC_SplicingNeoantigens/`
4. Ensure raw fastq inputs for Hugo (SRP070710), Riaz (SRP094781), and Gide (PRJEB23709) are accessible via SRA/ENA
5. Run cells in order. The full pipeline takes approximately 20 to 30 hours of compute time distributed across multiple Colab sessions.

## Substitutions and deviations from canonical implementations

Documented in the manuscript Methods and Supplementary Section 1:

- **LeafCutter-DS (Python and pyro)** instead of the R and Stan reference LeafCutter (compilation issues on Colab; Dirichlet-multinomial GLM and LRT unchanged) — amendment v5.4.3
- **Mann-Whitney U orthogonal validation** instead of Bisbee (installation failure on Colab; concordance threshold of 80 percent preserved) — amendment v5.4.7
- **MHCnuggets 2.4.0 with Keras 3 source patches** for compatibility with newer TensorFlow — see `../environment/mhcnuggets_keras3_patch.md`
- **SpliceMutr-adapted SA score with three documented deviations**: ORF cutoff instead of LGC, class II 15-mer extension, no default purity normalization — amendment v5.4.12
