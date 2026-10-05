# Experiment Proposal

## Research Question

Does increasing classification-head dropout reduce overfitting on our text
classifier without a meaningful loss in validation accuracy?

## Previous Findings

- `archive/2026-01-03-bert-base-text-classifier` established the current
  baseline: `bert-base-uncased` + linear head, dropout `0.1`, val accuracy
  `0.861`, train accuracy `0.942` (gap `8.1pp`).
- The gap was flagged as an open question in that change's follow-ups:
  "train/val gap is large relative to dataset size; worth testing standard
  regularization levers before trying architectural changes."

## Hypothesis

Increasing head dropout from `0.1` to `0.3` reduces the train/val accuracy
gap by at least 2 percentage points, without reducing validation accuracy by
more than 0.5 percentage points.

## Proposed Variant

Same baseline model and training setup; only the dropout rate applied before
the final linear classification layer changes from `0.1` to `0.3`.

## Expected Outcome

Train/val gap shrinks measurably (less overfitting) while val accuracy stays
within noise of the baseline — i.e., the baseline is leaving accuracy on the
table by overfitting the training set.

## Why This Experiment Now

Dropout is the cheapest, lowest-risk lever to test before considering
architectural changes (e.g. a smaller head, data augmentation, or early
stopping changes) raised as alternatives in the baseline change's follow-ups.

## Related Experiments

- `archive/2026-01-03-bert-base-text-classifier` (baseline this change
  compares against)
