# Worked example: `add-dropout-regularization`

A filled-out, fictional example of the full `ml-research` lifecycle, from
proposal to a synced spec. Numbers are made up but internally consistent;
the point is the *shape* of the artifacts and the discipline, not the
specific result.

- [`add-dropout-regularization/proposal.md`](add-dropout-regularization/proposal.md) — falsifiable hypothesis, referencing a prior (also fictional) baseline change
- [`add-dropout-regularization/design.md`](add-dropout-regularization/design.md) — single changed variable, everything else controlled
- [`add-dropout-regularization/evaluation.md`](add-dropout-regularization/evaluation.md) — success **and** falsification conditions defined before running anything
- [`add-dropout-regularization/tasks.md`](add-dropout-regularization/tasks.md) — executable checklist, including the exact commands run
- [`add-dropout-regularization/results.md`](add-dropout-regularization/results.md) — Results → Observations → Interpretation → Conclusion → Decision → Follow-ups
- [`specs/model-training/spec.md`](specs/model-training/spec.md) — the durable finding synced into the knowledge base at archive time

The interesting part: the hypothesis is **rejected** by its own
pre-registered falsification condition (the gap did shrink, but accuracy
dropped more than the plan allowed to call it a win). The schema's point is
that this is still a valuable, recorded finding — `specs/model-training/spec.md`
captures "dropout stays at 0.1 and why," not just the passing experiments.

This directory is a reference, not part of the installable schema. Only
`openspec/schemas/ml-research/` needs to be copied into a project.
