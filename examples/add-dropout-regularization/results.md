# Results

## 1. Results

| Config | Seed | Val Accuracy | Train Accuracy | Train/Val Gap |
|---|---|---|---|---|
| baseline (dropout 0.1) | 17 | 0.863 | 0.941 | 7.8pp |
| baseline (dropout 0.1) | 23 | 0.859 | 0.944 | 8.5pp |
| baseline (dropout 0.1) | 41 | 0.861 | 0.940 | 7.9pp |
| **baseline mean ± std** | — | **0.861 ± 0.002** | 0.942 ± 0.002 | **8.1 ± 0.4pp** |
| variant (dropout 0.3) | 17 | 0.850 | 0.891 | 4.1pp |
| variant (dropout 0.3) | 23 | 0.847 | 0.894 | 4.7pp |
| variant (dropout 0.3) | 41 | 0.846 | 0.887 | 4.1pp |
| **variant mean ± std** | — | **0.848 ± 0.002** | 0.891 ± 0.004 | **4.3 ± 0.3pp** |

Val accuracy delta (variant − baseline): **−1.3pp** (std-separated: both
3-seed ranges are disjoint).
Train/val gap delta: **−3.8pp** (gap shrank, std-separated).

### Slice: short (<20 tokens) vs. long reviews

| Config | Short review acc. | Long review acc. |
|---|---|---|
| baseline (mean) | 0.831 | 0.869 |
| variant (mean) | 0.796 | 0.861 |

### Success criteria (`evaluation.md`)

| # | Criterion | Result |
|---|---|---|
| 1 | Gap reduced by >= 2.0pp | **met** (3.8pp) |
| 2 | Val accuracy drop <= 0.5pp | **not met** (−1.3pp) |

## 2. Observations

- The accuracy drop is concentrated in the short-review slice (−3.5pp) vs.
  the long-review slice (−0.8pp); short inputs have fewer tokens for dropout
  to "spare," so a higher rate removes a larger fraction of the signal per
  example.
- All three seeds show the same direction and similar magnitude for both the
  accuracy drop and the gap reduction — this is not a single bad run.
- Train accuracy also dropped substantially (−5.1pp), consistent with
  dropout `0.3` constraining capacity more broadly, not just closing the
  generalization gap.

## 3. Interpretation

The train/val gap shrank as hypothesized, but it shrank because training
accuracy fell, not because validation accuracy improved — the model is
regularized more, but it is also worse. This matches the explicit
falsification condition in `evaluation.md` ("a shrinking gap bought with a
larger accuracy loss is not a win"), rather than the supported-hypothesis
condition. The slice breakdown suggests the mechanism is capacity reduction
on short inputs specifically, not a general overfitting fix.

## 4. Conclusion

Dropout `0.3` on the classification head is **not** an improvement over
`0.1`: it trades 1.3pp of validation accuracy for a smaller train/val gap,
and the loss is disproportionately borne by short reviews. The hypothesis as
stated ("gap shrinks without a meaningful accuracy loss") is rejected by the
pre-registered falsification condition, even though the gap-reduction half
of it held.

## 5. Decision

- Keep head dropout at `0.1` in the reference configuration. Do not adopt
  `0.3`.
- The train/val gap at `0.1` is not addressed by this lever; it remains an
  open problem for a future experiment using a different approach (see
  follow-ups).

## 6. Follow-up Questions

1. Does a smaller step (`head_dropout=0.2`) land between these two points, or
   is the accuracy cost non-linear in dropout rate?
2. Is the short-review accuracy drop specific to dropout, or would other
   regularizers (e.g. label smoothing) show the same slice-skew?
3. The original gap (8.1pp at dropout 0.1) is still unexplained — is it
   driven by dataset size, label noise, or genuine overfitting? Worth a
   dedicated data-scaling experiment before trying more regularization
   levers.
