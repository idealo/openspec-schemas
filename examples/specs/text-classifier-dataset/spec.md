## Purpose

Single source of truth for every dataset and split used by the text
classifier experiments — how each was generated, its statistics, and what
it can and cannot tell us.

## Code State

`data/make_splits.py` reads the raw review dump, deduplicates by review ID
and writes a label-stratified 80/10/10 split (seed `0`) to
`data/splits/reviews-sentiment-v2/{train,val,test}.csv`. Training and
evaluation scripts only read these CSVs; none of them re-split.

## Datasets

| Name | Size (train / val / test) | Role | ID / OOD | How generated | Statistics | What it implies |
|---|---|---|---|---|---|---|
| `reviews-sentiment-v2` | 48,213 / 6,027 / 6,031 | primary train/eval set; the test split is the fixed comparison split for all standard-table rows | ID | `data/make_splits.py`, stratified 80/10/10, seed 0 ([2026-01-03-bert-base-text-classifier](../../changes/archive/2026-01-03-bert-base-text-classifier/results.md)) | binary labels, 54% positive / 46% negative in every split; 18% of reviews are short (<20 tokens) | Comparisons across experiments are valid on test; no OOD set exists, so generalization beyond this review source is untested. |

## Requirements

### Requirement: Finding: reviews-sentiment-v2 splits are fixed and shared by all experiments

Experiments SHALL reuse the `reviews-sentiment-v2` split files verbatim and MUST NOT re-split.

#### Evidence: BERT-base classifier (BERT-B)

- **WHEN** the split is generated once with `data/make_splits.py` (stratified, seed 0)
- **THEN** 48,213 / 6,027 / 6,031 reviews, 54% positive in each split — [bert-base-text-classifier](../../changes/archive/2026-01-03-bert-base-text-classifier/results.md)
