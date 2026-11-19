## Purpose

Validated knowledge about training configuration choices for the text
classifier — which hyperparameters and regularization settings are
established as the reference configuration, and why.

## Code State

`model/head.py::ClassificationHead` wraps the pooled encoder output in a
single linear layer with a configurable dropout (`head_dropout`,
default `0.1`) applied before the linear layer. `conf/train.yaml` exposes
`model.head_dropout` as a training-time override; `train.py` reads it and
passes it to `ClassificationHead` unchanged — no other code path currently
reads this value.

## Datasets

See [`text-classifier-dataset`](../text-classifier-dataset/spec.md) —
all runs below use `reviews-sentiment-v2`.

## Experiments

| Acronym | Descriptive Name | Type | Hypothesis | Result (1 sentence) | Change |
|---|---|---|---|---|---|
| BERT-B | BERT-base classifier | experiment | none (baseline) | Established the reference classifier with head dropout 0.1 and an 8.1pp train/val gap. | [2026-01-03-bert-base-text-classifier](../../changes/archive/2026-01-03-bert-base-text-classifier/results.md) |
| HD-0.3 | Head dropout 0.3 | experiment | Dropout 0.3 shrinks the train/val gap by >=2pp at <=0.5pp val accuracy cost | Rejected: the gap shrank by 3.8pp, but val accuracy fell by 1.3pp. | [2026-01-20-add-dropout-regularization](../../changes/archive/2026-01-20-add-dropout-regularization/results.md) |

## Evaluation Metrics Overview

### Standard Table

All rows: test split of `reviews-sentiment-v2`, argmax scoring.

| Experiment | Variant | Setting | Scoring | Micro P | Micro R | Micro F1 | Macro P | Macro R | Macro F1 | Evidence |
|---|---|---|---|---|---|---|---|---|---|---|
| bert-base-text-classifier | BERT-B – BERT-base classifier | test, seed 17 | argmax | 0.857 | 0.857 | 0.857 | 0.855 | 0.851 | 0.853 | [results](../../changes/archive/2026-01-03-bert-base-text-classifier/results.md) |
| add-dropout-regularization | BERT-B – BERT-base classifier (re-run) | test, 3-seed mean | argmax | 0.858 | 0.858 | 0.858 | 0.856 | 0.852 | 0.854 | [results](../../changes/archive/2026-01-20-add-dropout-regularization/results.md) |
| add-dropout-regularization | HD-0.3 – Head dropout 0.3 | test, 3-seed mean | argmax | 0.845 | 0.845 | 0.845 | 0.843 | 0.836 | 0.839 | [results](../../changes/archive/2026-01-20-add-dropout-regularization/results.md) |

### Additional Metrics

| Run | Metric | Value | Evidence |
|---|---|---|---|
| BERT-B (re-run) | val accuracy / train/val gap | 0.861 ± 0.002 / 8.1 ± 0.4pp | [results](../../changes/archive/2026-01-20-add-dropout-regularization/results.md) |
| HD-0.3 | val accuracy / train/val gap | 0.848 ± 0.002 / 4.3 ± 0.3pp | [results](../../changes/archive/2026-01-20-add-dropout-regularization/results.md) |
| HD-0.3 vs. BERT-B | short / long review accuracy delta | −3.5pp / −0.8pp | [results](../../changes/archive/2026-01-20-add-dropout-regularization/results.md) |

## Requirements

### Requirement: Finding: Head dropout 0.3 costs more accuracy than it buys in generalization

The reference configuration SHALL keep `head_dropout=0.1`.

#### Evidence: Head dropout 0.3 (HD-0.3)

- **WHEN** head dropout is raised from 0.1 to 0.3 on `reviews-sentiment-v2`, 3 seeds, all else fixed
- **THEN** val accuracy −1.3pp (0.861 → 0.848), train/val gap −3.8pp, short reviews −3.5pp — [add-dropout-regularization](../../changes/archive/2026-01-20-add-dropout-regularization/results.md)
