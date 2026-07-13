# Pre-registration amendment record

This directory contains the key pre-registration amendments locked during the analysis. Each amendment was committed to this repository with a dated timestamp and a code-visible reason **before any pass-fail outcome was observed**. Where amendments involved substitutions of tools or paradigms that became necessary because of environment or data availability constraints, the substitution was locked in writing before the substituted computation was run.

The seven amendments preserved here document the methodological choices, substitutions, and sensitivity analyses that a reviewer would want to verify. The full 26-amendment sequence including QC lockdowns and cohort-selection decisions is available in the Git commit history for this directory.

## Amendment index

| Amendment | Date (2026) | Summary |
|-----------|-------------|---------|
| [v5.4.3](amendment_v5.4.3.md) | 11 Jun | LeafCutter-DS Python re-implementation formally locked (substitution rationale) |
| [v5.4.7](amendment_v5.4.7.md) | 13 Jun | Bisbee unavailability documented; Mann-Whitney U substitute locked |
| [v5.4.10](amendment_v5.4.10.md) | 14 Jun | Primary validation paradigm re-scoped to three-cohort independent replication |
| [v5.4.11](amendment_v5.4.11.md) | 14 Jun | Peptide prediction pipeline locked; 20 dual-class discovery threshold locked |
| [v5.4.12](amendment_v5.4.12.md) | 15 Jun | SpliceMutr-adapted SA score formula locked; three deviations documented |
| [v5.4.15](amendment_v5.4.15.md) | 18 Jun | Hugo tumor-purity sensitivity: stable (verified) |
| [v5.4.16](amendment_v5.4.16.md) | 18 Jun | Class II IC50 threshold sensitivity: robust 20 of 20 (verified) |

## Full audit trail

The Git commit history for this directory constitutes the audit trail with commit hashes and precise timestamps. To view:

```bash
cd pre_commitments
git log --pretty=format:"%h %ad %s" --date=iso .
```

## What is NOT in this directory

Nineteen other amendments in the original sequence covered QC lockdowns, cohort selection decisions, and incremental infrastructure refinements (STAR parameter corrections, Salmon dropped, sample list corrections, etc.). These are documented in the manuscript Methods and Supplementary Section 1 rather than as standalone files here, since they do not affect result interpretation.
