# Experiment Tasks

## Implementation

- [x] Add `head_dropout` override to `conf/train.yaml` and the model
      constructor; verify default (`0.1`) reproduces the baseline's reported
      val accuracy within noise on seed `17`.
- [x] Add a unit test asserting the head's dropout module uses the
      configured rate (`tests/test_model_head.py`).

## Experiment

- [x] Run baseline (`head_dropout=0.1`), seeds 17/23/41:
      `python train.py model.head_dropout=0.1 seed={17,23,41}`.
- [x] Run variant (`head_dropout=0.3`), seeds 17/23/41:
      `python train.py model.head_dropout=0.3 seed={17,23,41}`.
- [x] Store configs and run folders under `runs/add-dropout-regularization/`.

## Evaluation

- [x] Compute val accuracy and train/val gap per run; aggregate mean ± std
      per configuration: `python evaluate.py --run-glob "runs/add-dropout-regularization/*"`.
- [x] Compute short/long review slice accuracy for both configurations.
- [x] Check success criteria from `evaluation.md` against the aggregated
      numbers.

## Documentation

- [x] Create `results.md`.
- [x] Record numerical results (per-seed and aggregated).
- [x] Record factual observations (slice behavior, variance).
- [x] Interpret findings against the success/falsification criteria.
- [x] State whether the hypothesis was supported.
- [x] Record decision (keep baseline dropout, or adopt variant).
- [x] Record possible follow-up experiments.
- [x] Distill the durable finding into
      `openspec/specs/model-training/spec.md` (this change does not qualify
      for `skip_specs: true` — a dropout decision is durable, even though the
      hypothesis was rejected).
