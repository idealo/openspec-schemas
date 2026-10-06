# ml-research — OpenSpec community schema

This repository adapts [OpenSpec](https://github.com/Fission-AI/OpenSpec), a
spec-driven development framework, to machine-learning research. Hypothesis
(the why), design (the how), evaluation plan (how we measure) and tasks (the
what) are captured as Markdown before an experiment runs, so that humans and AI
coding agents can plan, execute, document and iterate on experiments with a
traceable research history. It is the practical foundation for the blog post
*"AI assisted Research with OpenSpec: From Spec-Driven Development to
Spec-Driven ML Research"*.

## The Missing Layer in ML Experiment Tracking

Tools like MLflow or Weights & Biases store metrics, models and datasets, but
answering *why* an experiment was run and *what was learned* from it a year
later is much harder. This schema adds that missing layer: a structured,
traceable record of hypothesis, design, evaluation plan and decision for every
experiment.

## What's in this repo

- [`openspec/schemas/ml-research/`](openspec/schemas/ml-research) — the schema
  and its artifact templates
- [`examples/`](examples) — a worked example of a full experiment lifecycle

## Overview

An [OpenSpec](https://github.com/Fission-AI/OpenSpec) workflow schema for
iterative machine-learning research. It extends OpenSpec's default
`proposal → design → tasks` flow with an **evaluation** artifact and a
results-first **specs** convention, so that:

- success criteria are fixed *before* an experiment runs,
- results, interpretation and decision are kept separate and never silently
  overwrite the original hypothesis,
- only evidence-backed findings — including refuted hypotheses — become
  durable knowledge in `openspec/specs/`.

## Install

Copy the schema bundle into your project:

```bash
cp -r openspec/schemas/ml-research <your-project>/openspec/schemas/
```

Then point your project at it in `openspec/config.yaml`:

```yaml
schema: ml-research
```

Validate it resolves correctly:

```bash
openspec schema validate ml-research
```

## Workflow

| Artifact | Written | Purpose |
|---|---|---|
| `proposal.md` | before the experiment | research question, prior findings, **falsifiable** hypothesis, expected outcome |
| `design.md` | before the experiment | baseline vs. variant, changed vs. controlled variables, model/data/training setup, seeds, reproducibility |
| `evaluation.md` | before the experiment | primary/secondary metrics, baseline comparison, slices, ablations, success criteria, falsification condition |
| `tasks.md` | before execution | concrete, executable steps (incl. exact script calls/parameters) covering implementation → run → evaluation → `results.md` → specs |
| `results.md` | after the experiment | strictly separated: Results, Observations, Interpretation, Conclusion, Decision, Follow-up Questions |
| `specs/<capability>/spec.md` | during/after results | only the durable, evidence-backed finding — as a `### Requirement: Finding: <name>` with a linked `#### Evidence:` (WHEN/THEN) block |

Standard OpenSpec commands drive this (`/opsx:propose`, `/opsx:apply`,
`/opsx:archive`, or your agent's generated skills) — only the artifacts and
their instructions are specific to this schema.

Key rules enforced by the schema's instructions:

- The hypothesis in `proposal.md` is never rewritten after seeing results.
- A refuted hypothesis is still a finding worth recording (e.g. "approach X
  degrades OOD generalization — do not use it").
- `specs/` is written **post-results**, never up front — it records the
  decision, not the untested hypothesis.
- Use `skip_specs: true` only when an experiment established nothing durable
  at all (pure tooling, aborted run, no interpretable evidence).

## Example `config.yaml` additions

Optional project-level context/rules that complement the schema (adjust to
your project):

```yaml
schema: ml-research

context: |
  This repository contains iterative machine-learning research.
  Experiments should build on previous experimental evidence.
  When previous related experiments exist, inspect them before
  proposing a new experiment.

rules:
  proposal:
    - Reference relevant previous experiments whenever possible.
    - Prefer falsifiable hypotheses.
  specs:
    - Record findings post-results, never the untested hypothesis.
    - A refuted hypothesis is still a finding worth recording.

operations:
  archive:
    guidance:
      - Ensure results.md contains the final results and conclusion.
      - Sync the experiment's finding into the knowledge base (openspec/specs/).
```

## License

MIT, see [LICENSE](LICENSE).
