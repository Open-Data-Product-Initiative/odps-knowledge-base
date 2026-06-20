# ODPR Recipe Examples

These examples show the main recipe workflow shapes:

- `ci-validate-catalog.yaml`: deterministic validation that can execute.
- `portfolio-sync-render.yaml`: deterministic portfolio sync, render, and
  explain flow that writes only under `workspace/`.
- `generate-signal.yaml`: LLM-backed ODPC signal fragment generation with
  provider readiness, explicit LLM permission, and review approval.
- `odpg-build.yaml`: LLM-backed ODPG graph build from ODPC fragments with
  provider readiness, explicit LLM permission, and review approval.
- `portfolio-build.yaml`: LLM-backed portfolio build from source lane notes
  with provider readiness, explicit LLM permission, and review approval.
- `portfolio-refresh.yaml`: LLM-backed portfolio refresh from source lane notes
  with provider readiness, explicit LLM permission, and review approval.
- `release-portfolio-localize.yaml`: LLM-backed release localization that is
  guarded by provider readiness, explicit LLM permission, and review approval.

Run from the repository root:

```bash
open-data-products recipe validate sdk/recipes/workflows/ci-validate-catalog.yaml --json
open-data-products recipe run sdk/recipes/workflows/ci-validate-catalog.yaml \
  --config sdk/recipes/config/recipes.config.yaml \
  --dry-run \
  --json
open-data-products recipe run sdk/recipes/workflows/ci-validate-catalog.yaml \
  --config sdk/recipes/config/recipes.config.yaml \
  --execute \
  --json
```

The example config sets `workflows/ci-validate-catalog.yaml` as
`recipes.defaultRecipe`, so the dry-run can also be started without a recipe
path:

```bash
open-data-products recipe run \
  --config sdk/recipes/config/recipes.config.yaml \
  --dry-run \
  --json
```

For the LLM-backed release example, inspect the dry-run first:

```bash
open-data-products recipe run sdk/recipes/workflows/release-portfolio-localize.yaml \
  --config sdk/recipes/config/recipes.config.yaml \
  --dry-run \
  --json
```

For the LLM-backed graph and portfolio examples, inspect the dry-run first:

```bash
open-data-products recipe run sdk/recipes/workflows/generate-signal.yaml \
  --config sdk/recipes/config/recipes.config.yaml \
  --dry-run \
  --json
open-data-products recipe run sdk/recipes/workflows/odpg-build.yaml \
  --config sdk/recipes/config/recipes.config.yaml \
  --dry-run \
  --json
open-data-products recipe run sdk/recipes/workflows/portfolio-build.yaml \
  --config sdk/recipes/config/recipes.config.yaml \
  --dry-run \
  --json
open-data-products recipe run sdk/recipes/workflows/portfolio-refresh.yaml \
  --config sdk/recipes/config/recipes.config.yaml \
  --dry-run \
  --json
```

Execute any workflow only after reviewing the dry-run plan:

```bash
open-data-products recipe run sdk/recipes/workflows/odpg-build.yaml \
  --config sdk/recipes/config/recipes.config.yaml \
  --execute \
  --allow-llm \
  --approve-review \
  --json
open-data-products recipe run sdk/recipes/workflows/portfolio-build.yaml \
  --config sdk/recipes/config/recipes.config.yaml \
  --execute \
  --allow-llm \
  --approve-review \
  --json
open-data-products recipe run sdk/recipes/workflows/portfolio-refresh.yaml \
  --config sdk/recipes/config/recipes.config.yaml \
  --execute \
  --allow-llm \
  --approve-review \
  --json
```

The dry-run reports provider readiness from
`sdk/recipes/config/generation.config.yaml`. If `ANTHROPIC_API_KEY` is not set,
the provider readiness is `missing-env`. Execute mode blocks LLM-backed steps
until the selected provider is ready and both guard flags are present.
