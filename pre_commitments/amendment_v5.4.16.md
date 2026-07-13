# Amendment v5.4.16

**Date:** 18 June 2026
**Summary:** Class II IC50 threshold sensitivity locked

## Full record

Class II IC50 threshold sensitivity analysis locked in writing before computation. Tightened class II threshold from 1000 nM (canonical MHCnuggets recommendation for class II) to 500 nM (matching class I). Purpose: test whether the 20-cluster-tuple discovery outcome is robust to a stringent class II calibration. Pre-specified pass criterion: at least 15 of 20 dual-class cluster-tuples retained under the tightened threshold.

## Result

Executed as cell `L2-PATH-Y2-FIX-CLASSII-IC50-500-SENSITIVITY` on 18 June 2026 at 03:45 UTC. At the tighter class II threshold, binder records dropped from 19,520 to 12,374 (-36.6 percent), unique peptides from 855 to 738 (-13.7 percent). Unique alleles unchanged at 96. Class II cluster-tuples with binders unchanged at 20. Class I cluster-tuples unchanged at 20. Dual-class cluster-tuples: 20 (1000 nM) → 20 (500 nM).

**Verdict:** `robust_to_threshold`
**Interpretation:** Discovery PASS is robust to tighter class II threshold. At IC50 less than 500 nM, 20 of original 20 dual-class cluster-tuples retained (100 percent). Zero cluster-tuples lost. Charter v5.4.11 outcome confirmed.

All 21 gene symbols retained under the tightened threshold: ANKRD10, APOO, ARMC10, B4GALT7, CNIH3, CNIH4, ELOVL1, MED8, GAS7, IRAK4, JMJD8, KRBOX5, LYST, MINDY1, OARD1, PTPRM, RER1, SMIM14, TVP23C-CDRT4, UBR4, UPF3A (21 genes across 20 cluster-tuples; ELOVL1 and MED8 share one cluster-tuple).

## Output files

Archived at `data/stage2_outputs/_story_a/path_y/` in the project Drive:

- `binders_classII_500nM.csv` (444.9 KB)
- `comparison_1000_vs_500.csv` (0.3 KB)
- `passfail_classII_500_sensitivity.json` (0.9 KB)

## Related files

- Pre-commitment archive: this file (git commit hash is the timestamp of record)
- Executed in notebook cell: `L2-PATH-Y2-FIX-CLASSII-IC50-500-SENSITIVITY` (Stage 12 of the pipeline notebook)
- Referenced in manuscript Methods, Supplementary Section 1.7
- Related amendments listed in [README.md](README.md)
