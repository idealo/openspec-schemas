# Worked example: `add-dropout-regularization`

A filled-out, fictional example of the full `ml-research` lifecycle, from
proposal to a synced spec. Numbers are made up but internally consistent;
the point is the *shape* of the artifacts and the discipline, not the
specific result.

- [`add-dropout-regularization/proposal.md`](add-dropout-regularization/proposal.md) — name + acronym ("Head dropout 0.3 (HD-0.3)"), type `experiment`, falsifiable hypothesis, referencing a prior (also fictional) baseline change
- [`add-dropout-regularization/design.md`](add-dropout-regularization/design.md) — single changed variable, everything else controlled
- [`add-dropout-regularization/evaluation.md`](add-dropout-regularization/evaluation.md) — micro/macro metrics, a fixed evaluation setting, and success **and** falsification conditions defined before running anything
- [`add-dropout-regularization/tasks.md`](add-dropout-regularization/tasks.md) — executable checklist, including the exact commands run
- [`add-dropout-regularization/results.md`](add-dropout-regularization/results.md) — standard metrics table first, then Results → Observations → Interpretation → Conclusion → Decision → Follow-ups
- [`specs/model-training/spec.md`](specs/model-training/spec.md) — the capability summary after archiving: Experiments registry, standard metrics table, and the short finding
- [`specs/text-classifier-dataset/spec.md`](specs/text-classifier-dataset/spec.md) — the single dataset spec that every other spec links to for `## Datasets`

The interesting part: the hypothesis is **rejected** by its own
pre-registered falsification condition (the gap did shrink, but accuracy
dropped more than the plan allowed to call it a win). The schema's point is
that this is still a valuable, recorded finding — `specs/model-training/spec.md`
captures "dropout stays at 0.1 and why," not just the passing experiments.

The specs link to `../../changes/archive/...` as they would inside a real
project's `openspec/specs/`. Those links do not resolve in this repository.

This directory is a reference, not part of the installable schema. Only
`openspec/schemas/ml-research/` needs to be copied into a project.
