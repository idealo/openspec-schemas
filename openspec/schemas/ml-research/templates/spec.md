## Purpose
<!-- New capabilities only: one or two sentences (50+ chars) on which body of validated knowledge this capability covers. Delete this section when adding to an existing capability. -->

## Code State
<!-- Plain factual description of what the capability's code currently does: relevant modules/functions and how they fit together (e.g. "masking/shared_mask.py implements the plain-[MASK] baseline; training/trainer.py::build_trainer wires it into the HF Trainer"). Edit in place whenever the code changes - this is not a delta and not evidence-backed, just the current state. -->

## Datasets
<!-- Only in the <project_name> dataset spec; other specs link there. Edited directly. Per dataset/split: name, size, role, ID/OOD, how generated (script, sampling, link to archived change), statistics, what it implies. -->

## Experiments
<!-- Edited directly. | acronym | descriptive name | typ | hypothesis (or "none") | result (1 sentence) | change (link) | -->

## Evaluation Metrics Overview
<!-- Edited directly in openspec/specs/, not a delta. Standard-Table (one row per variant, all columns mandatory):
| Experiment | Variante (`Acronym – descriptive name`) | Setting | Scoring | Micro P | Micro R | Micro F1 | Macro P | Macro R | Macro F1 | Evidence |
|---|---|---|---|---|---|---|---|---|---|---|
Followed by "### additional metrics" (Run | Metric | Value | Evidence) for deltas, CIs, ablations, cost. -->

## ADDED Requirements

### Requirement: Finding: <!-- the finding itself as a short statement, e.g. "Per-root-group fine-tuning gives a small, consistent gain" -->
<!-- ONE sentence: the resulting decision, with MUST/SHALL. Whole block < ~500 chars; details stay in results.md. -->

#### Evidence: <!-- descriptive name of the experiment -->
- **WHEN** <!-- what was tried, on which data/split (one line) -->
- **THEN** <!-- key number(s) (one line) --> — [<change>](../../changes/archive/YYYY-MM-DD-<change-name>/results.md)
