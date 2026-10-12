# Contributing

We welcome any contributions for helping improve the `ml-research` OpenSpec schema. This guide
explains how to propose and submit changes.

## Ways to contribute

- Report a bug or unclear instruction in the schema or its templates
- Suggest improvements to the workflow (new artifacts, better instructions)
- Improve the documentation or the worked example in [`examples/`](examples)

For larger changes, please open an issue first so we can agree on the
direction before you invest time.

## What lives where

| Path | Purpose |
|---|---|
| `openspec/schemas/ml-research/schema.yaml` | artifact definitions, dependencies and instructions |
| `openspec/schemas/ml-research/templates/` | Markdown templates for each artifact |
| `examples/` | worked example of a full experiment lifecycle (reference only, not installed) |

## Development setup

1. Install [OpenSpec](https://github.com/Fission-AI/OpenSpec).
2. Install [pre-commit](https://pre-commit.com) and enable the hooks:

   ```bash
   pre-commit install
   ```

   The hooks run [gitleaks](https://github.com/gitleaks/gitleaks) to prevent
   secrets from being committed.

## Making changes

All changes must be made through a **fork**. Please do not push branches
directly to this repository.

1. [Fork](https://github.com/idealo/openspec-schemas/fork) the repository and
   clone your fork:

   ```bash
   git clone git@github.com:<your-user>/openspec-schemas.git
   cd openspec-schemas
   git remote add upstream git@github.com:idealo/openspec-schemas.git
   ```

2. Create a branch from an up-to-date `main`, e.g. `feature/<short-description>`
   or `fix/<short-description>`:

   ```bash
   git fetch upstream
   git checkout -b feature/<short-description> upstream/main
   ```

3. Make your change. When you touch the schema, keep these in sync:
   - `schema.yaml` and the matching file in `templates/`
   - the workflow table and rules in the [README](README.md)
   - the worked example in `examples/`, if the artifact structure changes
4. Validate the schema:

   ```bash
   openspec schema validate ml-research
   ```

5. Commit with a clear, imperative message (e.g. `add evaluation slices section`).
6. Push the branch to your fork and open a pull request from it against
   `main` of `idealo/openspec-schemas`.

## Pull requests

- Describe what changed and why.
- Link the related issue, if there is one.
- Make sure `openspec schema validate ml-research` passes.
- Reviews are requested automatically from the code owners listed in
  [`CODEOWNERS`](CODEOWNERS).

## License

By contributing, you agree that your contributions are licensed under the
[MIT License](LICENSE).
