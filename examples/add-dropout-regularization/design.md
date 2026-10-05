# Experiment Design

## Baseline

`bert-base-uncased` encoder, mean-pooled, single linear classification head,
head dropout `0.1`. Trained for 5 epochs, batch size 32, lr `2e-5`, AdamW,
linear warmup 10%. Dataset: `reviews-sentiment-v2` (train 48,213 / val 6,027
/ test 6,031).

## Experimental Variant

Identical setup; head dropout changed from `0.1` to `0.3`.

## Changed Variables

- Head dropout rate (`0.1` → `0.3`).

## Controlled Variables

- Model/encoder, tokenizer, max sequence length (128).
- Learning rate, batch size, optimizer, warmup schedule, epochs.
- Dataset, split, and preprocessing.
- Random seeds (same 3 seeds for baseline and variant).

## Model

`bert-base-uncased` (unchanged), 1 linear layer head, 2 output classes.

## Dataset

`reviews-sentiment-v2`, same split as the baseline change. No new data.

## Data Splits

Reused verbatim from `archive/2026-01-03-bert-base-text-classifier`
(`data/splits/reviews-sentiment-v2/{train,val,test}.csv`).

## Training Configuration

5 epochs, batch size 32, lr `2e-5`, AdamW, linear warmup 10%, fp16.

## Hyperparameters

Only `head_dropout` differs between runs (`0.1` baseline vs `0.3` variant).

## Random Seeds

Seeds `17`, `23`, `41` for both baseline and variant (baseline reruns use the
same seeds for a fair paired comparison rather than reusing the single-seed
numbers from the earlier change).

## Experiment Tracking

Local run folders under `runs/add-dropout-regularization/<seed>/`, metrics
logged to `runs/.../metrics.json`.

## Reproducibility

Git commit of this change, `conf/train.yaml` with `head_dropout` overridden
per run, fixed seeds, pinned `transformers`/`torch` versions from
`requirements.txt`.
