# Video Script: Zero-Shot Coastal Bacteria Ranker - Data Scientist Version

Source artifacts:
- bacteria_results/international/unified_zero_shot_gauntlet.md
- bacteria_results/international/unified_zero_shot_physics_kernel_screen.md
- bacteria_results/international/unified_zero_shot_physics_kernel_screen.json
- research/bacteria/international/unified_zero_shot_gauntlet.py
- research/bacteria/international/interlingua_basins.py

## Scene 1: Title
This is the data scientist version of the zero-shot coastal bacteria result. It walks through the panel contract, PI feature engine, model protocol, nulls, gates, washouts, and limitations.

## Scene 2: Question
The research question was narrow: can a label-free model train on non-target basins and rank enterococcus exceedance in a completely held-out basin, with zero target-domain labels or lab-history features as inputs?

## Scene 3: Panel
The final scored panel had twelve domains, 708,337 held-out rows, and 57,628 events. Rows needed a date, site, basin, coordinates, a comparable daily bacteria label, and finite PI features.

## Scene 4: Source Quality
Data quality was enforced by exclusion, not wishful imputation. Empty Wales, annual-only EEA bathing class data, pre-2012 Montenegro, and Hong Kong without coordinates were excluded from daily PI transfer.

## Scene 5: Feature Contract
The anti-leak feature contract allowed weather, PI groups, calendar, optional geography, and optional strings for non-headline arms. It blocked FIB concentration, hazard labels, exceedance labels, lab-history lags, and target-domain labels.

## Scene 6: Pi Features
The headline feature set was five PI groups: Damkohler-style decay, loading, UV dose, Peclet-style transport, and flushing. These are shared physical coordinates rather than basin identity features.

## Scene 7: Physics Kernels
We also engineered compact label-free physics kernels from the same inputs: decay-adjusted load, solar survival load, runoff memory, first flush, flushing inverse, spring-neap exchange, transport retention, and wind resuspension.

## Scene 8: Model Zoo
The model zoo compared calendar, PI, PI plus calendar, raw physics, physics plus geography, physics-kernel variants, and sampled CARTE strings. The frozen public winner was PI plus logistic.

## Scene 9: Lobo
The validation split was leave-one-basin-out. For each target, the model trained only on rows from the other basins, then scored the hidden basin. This repeated across all twelve domains.

## Scene 10: Scoring
The primary metric was average precision, because the use case is ranking early sampling attention. The base-rate baseline is the held-out event rate; lift is AP divided by that base rate.

## Scene 11: Nulls
The null check was source-stratum permutation. Outcomes were shuffled within source buckets, preserving source mix, and the real AP had to beat the ninety-fifth percentile shuffled score. It did on all twelve targets.

## Scene 12: Bootstrap Gate
The freeze gate required every target above base rate, at least eighty percent above the permutation null, at least one hundred null draws per target, AP-minus-base bootstrap lower bound above zero, and mean-lift lower bound above one.

## Scene 13: Headline Result
The headline PI plus logistic result was mean AP 0.1511 versus mean base rate 0.0909, for mean lift 1.752. The domain-bootstrap AP-minus-base interval was 0.0365 to 0.086.

## Scene 14: Target Table
Per-target results were not one lucky basin. All twelve held-out domains beat their own base rate. The strongest lifts were Australia New South Wales, California, Ireland, and Texas; the weakest lift was North Carolina at 1.186.

## Scene 15: Kernel Wash
The richer physics-kernel arms looked tempting on mean AP, but they washed under the promotion rule. The best kernel added 0.0083 mean AP, but its paired-domain interval crossed zero and five targets regressed.

## Scene 16: Carte Limits
CARTE and entity-string variants were not frozen. Prior same-sample fair-baseline checks failed, and full-panel CARTE was too slow, so strings did not become part of the claim.

## Scene 17: Limits
The limitations matter. This is a retrospective zero-shot ranking screen, not a calibrated advisory probability. Persistence and seasonal-naive were not run because target-domain history is forbidden in the cold-start setting.

## Scene 18: Repro
The reproducibility artifacts are the runner, markdown and JSON outputs, freeze manifest, and test file. The caveat is that byte-reproduction from a clean clone is not yet proven because cached panels are not public frozen inputs.

## Scene 19: Closing
The defensible data-science claim is narrow: a simple PI plus logistic ranker clears a hardened zero-shot screen for prioritizing early sampling in unseen coastal bacteria basins.
