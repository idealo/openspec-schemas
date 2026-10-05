# Evaluation Plan

## Primary Metric

Validation accuracy (mean over 3 seeds).

## Secondary Metrics

- Train/val accuracy gap (mean over 3 seeds).
- Validation macro-F1 (sanity check against class imbalance effects).

## Baseline Comparison

Rerun baseline (dropout `0.1`) with the same 3 seeds as the variant, rather
than reusing the single-seed baseline number, so the comparison is paired and
not confounded by seed variance.

## Relevant Slices

- Short reviews (<20 tokens) vs. long reviews (>=20 tokens) — dropout affects
  short inputs disproportionately in prior internal experience.

## Ablations

None planned; single-variable change (dropout rate only).

## Success Criteria

- Train/val gap (variant) <= train/val gap (baseline) − 2.0pp, **and**
- val accuracy (variant) >= val accuracy (baseline) − 0.5pp.

## Hypothesis Supported If

Both success criteria above hold, with the gap reduction and accuracy
difference each outside their 3-seed standard deviation.

## Hypothesis Rejected If

Val accuracy (variant) drops by more than 0.5pp vs. baseline, regardless of
how much the train/val gap shrinks — a shrinking gap bought with a larger
accuracy loss is not a win for this hypothesis.

## Required Analysis

- Per-seed val accuracy and train/val gap (mean ± std).
- Short vs. long review slice accuracy, both configurations.
