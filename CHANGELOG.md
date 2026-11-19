# Changelog

All notable changes to the `ml-research` schema. Versions match the
`version:` field in [`schema.yaml`](openspec/schemas/ml-research/schema.yaml)
and the `ml-research-v<N>` git tags. Format based on
[Keep a Changelog](https://keepachangelog.com).

## [2] - 2026-11-19

### Added

- Change types `experiment`, `dataset` and `change` (`Type:` in the proposal).
- Descriptive name plus acronym for every change (`Name:` in the proposal).
- Spec sections `## Experiments` (registry of all changes) and a mandatory
  standard table in `## Evaluation Metrics Overview` (micro and macro P/R/F1
  for every variant on the same test split), followed by additional metrics.
- `## Evaluation Setting` in `evaluation.md`. Micro/macro P/R/F1 are always
  secondary metrics, and `results.md` starts with the same table.
- Dataset changes: evaluation and results report dataset statistics and
  quality checks instead of model metrics.

### Changed

- The hypothesis is optional. The agent always asks for one and never
  invents it. Without one, the proposal states "No hypothesis (reason)" and
  a research question or goal.
- `## Datasets` lives only in one dedicated dataset spec. Other specs link
  to it.
- Findings are short (one MUST/SHALL sentence, under ~500 characters). The
  header is the finding itself, and evidence links the archived
  `results.md`.

### Migration from v1

Existing specs stay valid for `openspec validate`, but lack the new
structure:

1. Move `## Datasets` content into a single `<project>-dataset` spec and
   replace it elsewhere with a link.
2. Add an `## Experiments` table with one row per archived change.
3. Convert `## Evaluation Metrics Overview` to the standard table. Where a
   v1 run lacks micro/macro numbers, note this in the row.
4. Optionally shorten long findings and move details into the linked
   `results.md`.

## [1] - 2026-10-05

Initial release: `proposal → design → evaluation → tasks → specs` workflow
with post-results findings and evidence blocks.
