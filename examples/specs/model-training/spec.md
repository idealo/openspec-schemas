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

- `reviews-sentiment-v2` — in-distribution, train 48,213 / val 6,027 / test
  6,031, binary sentiment labels. Role: primary training/eval dataset for
  the text classifier line of experiments.

## Evaluation Metrics Overview

| Change | Config | Val Accuracy | Train/Val Gap |
|---|---|---|---|
| `archive/2026-01-03-bert-base-text-classifier` | dropout 0.1, single seed | 0.861 | 8.1pp |
| `archive/2026-01-20-add-dropout-regularization` | dropout 0.1, 3-seed mean | 0.861 ± 0.002 | 8.1 ± 0.4pp |
| `archive/2026-01-20-add-dropout-regularization` | dropout 0.3, 3-seed mean | 0.848 ± 0.002 | 4.3 ± 0.3pp |

## Requirements

### Requirement: Finding: Classification head dropout stays at 0.1

Head dropout `0.3` reduces the train/val accuracy gap but costs more
validation accuracy than the gap reduction is worth, with the loss
concentrated on short-input examples. The reference configuration keeps
`head_dropout=0.1`. The train/val gap at this setting is not addressed by
this lever and remains an open problem (see the archived change's
follow-ups).

#### Evidence: add-dropout-regularization

- **WHEN** head dropout is raised from `0.1` to `0.3` on the
  `reviews-sentiment-v2` text classifier, 3 seeds each, all other
  hyperparameters held fixed (`archive/2026-01-20-add-dropout-regularization`)
- **THEN** validation accuracy drops by 1.3pp (0.861 → 0.848, std-separated
  across seeds) while the train/val gap shrinks by 3.8pp (8.1pp → 4.3pp);
  short-review accuracy drops more (−3.5pp) than long-review accuracy
  (−0.8pp)
