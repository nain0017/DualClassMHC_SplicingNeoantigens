# Amendment v5.4.15

**Date:** 18 June 2026
**Summary:** Hugo tumor-purity sensitivity locked

## Full record

Hugo tumor-purity sensitivity analysis locked in writing before computation. Scope limited to Hugo because external tumor purity is available only for Hugo in Patterson and Auslander 2022; Riaz and Gide are disclosed as data-availability limitations rather than imputed. Method: recompute SA score with per-gene expression divided by tumor purity, then repeat the primary discovery pipeline. Pre-specified pass criterion: direction of the top 20 cluster-tuples preserved (Spearman rho of ranked cluster-tuple order versus original at least 0.7).

## Result

Executed as cell `L2-PATH-Y1-FIX-v2` on 18 June 2026 at 03:50 UTC. Hugo tumor purity coverage: 26/26 samples (100%), median purity 0.590, range 0.140 to 0.890. Riaz 0/32 and Gide 0/34 disclosed as data availability limitations. Purity-normalized SA scores computed for Hugo samples. Mann-Whitney U (R vs NR) and Cox univariate (z-scored) executed for original SA versus purity-normalized SA across SA class I, SA class II, and SA combined.

**Verdict:** `stable_under_purity_normalization`
**Interpretation:** Hugo R vs NR direction and significance are stable under purity normalization. Charter v5.4.12 results for the Hugo cohort are robust to purity normalization.

## Output files

Archived at `data/stage2_outputs/_story_a/path_y/` in the project Drive:

- `hugo_purity_normalized_full.csv` (4.1 KB)
- `hugo_R_NR_purity_sensitivity.csv` (0.6 KB)
- `hugo_cox_purity_sensitivity.csv` (0.7 KB)
- `passfail_purity_hugo_only.json` (0.6 KB)

## Related files

- Pre-commitment archive: this file (git commit hash is the timestamp of record)
- Executed in notebook cell: `L2-PATH-Y1-FIX-v2` (Stage 12 of the pipeline notebook)
- Referenced in manuscript Methods, Supplementary Section 1.8
- Related amendments listed in [README.md](README.md)
