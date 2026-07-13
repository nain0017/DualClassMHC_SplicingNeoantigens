# Amendment v5.4.12

**Date:** 15 June 2026
**Summary:** SpliceMutr-adapted SA score formula locked

## Full record

SpliceMutr-adapted SA score formula locked: per-sample SA score = expression-weighted mean of per-gene modified-protein binder counts. Three deviations from canonical SpliceMutr acknowledged and documented: (1) ORF length cutoff of at least 30 amino acids instead of LGC coding-potential prediction (LGC requires species-specific training data not available for our GENCODE v45 build); (2) class II 15-mer extension (SpliceMutr canonical is class I only); (3) no purity normalization in the default score (addressed by pre-registered amendment v5.4.15 sensitivity analysis).

## Related files

- Pre-commitment archive: this file (git commit hash is the timestamp of record)
- Referenced in manuscript Methods, Supplementary Section 2
- Related amendments listed in [README.md](README.md)
