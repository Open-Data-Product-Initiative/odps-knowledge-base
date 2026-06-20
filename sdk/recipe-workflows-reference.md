# ODPR Recipe Workflows Reference

ODPR recipes describe repeatable SDK workflows. Use them when the same project
needs to validate, build, sync, render, localize, or review Open Data Products
artifacts in a predictable order.

## Why Use Recipe Workflows

Recipe workflows turn a set of manual SDK commands into a named, reviewable
runbook. This matters when Open Data Products work moves from one developer's
terminal into team operations, CI, release checks, portfolio publishing, or AI
agent automation.

The business benefits are:

- repeatability: the same validation, build, render, localization, and review
  steps run in the same order every time;
- governance: write scopes, review requirements, provider choices, and
  execution policy are visible before anything changes;
- release evidence: every execution attempt can leave a compact manifest that
  records what was attempted, what ran, what was blocked, and what artifacts
  need review;
- safer AI automation: agents can dry-run a recipe, inspect planned writes,
  provider readiness, blocking reasons, and review status before executing;
- separation of responsibilities: workflow owners can maintain recipes,
  platform owners can maintain runner policy, and LLM/provider owners can
  maintain `generation.config.yaml`;
- lower operational friction: recurring workflows become one command instead
  of a copied sequence of fragile shell commands.

Use recipes for workflows that need to be repeated, reviewed, delegated, or
automated. For a one-off local experiment, direct SDK commands are often
simpler.

## Starter Examples

The repository includes starter recipes under `sdk/recipes/`:

| Example | What it demonstrates |
| --- | --- |
| `sdk/recipes/workflows/ci-validate-catalog.yaml` | Deterministic catalog validation that can dry-run and execute. |
| `sdk/recipes/workflows/portfolio-sync-render.yaml` | Deterministic portfolio sync, render, and explain steps with writes limited to `workspace/`. |
| `sdk/recipes/workflows/odpg-build.yaml` | LLM-backed ODPG graph build from ODPC fragments, guarded by provider readiness, explicit LLM permission, and review approval. |
| `sdk/recipes/workflows/portfolio-build.yaml` | LLM-backed portfolio build from source lane notes, guarded by provider readiness, explicit LLM permission, and review approval. |
| `sdk/recipes/workflows/portfolio-refresh.yaml` | LLM-backed portfolio refresh from source lane notes, guarded by provider readiness, explicit LLM permission, and review approval. |
| `sdk/recipes/workflows/release-portfolio-localize.yaml` | LLM-backed release localization that dry-runs with provider readiness and review status, then executes only with explicit LLM and review approval. |

The example runner config is `sdk/recipes/config/recipes.config.yaml`.
The example provider config is `sdk/recipes/config/generation.config.yaml`.

Run the deterministic validation example:

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

Because the example config sets `recipes.defaultRecipe`, you can also omit the
recipe path:

```bash
open-data-products recipe run \
  --config sdk/recipes/config/recipes.config.yaml \
  --dry-run \
  --json
```

Dry-run the LLM-backed release example:

```bash
open-data-products recipe run sdk/recipes/workflows/release-portfolio-localize.yaml \
  --config sdk/recipes/config/recipes.config.yaml \
  --dry-run \
  --json
```

Dry-run the LLM-backed graph and portfolio examples:

```bash
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

If `ANTHROPIC_API_KEY` is not set, the dry-run reports provider readiness as
`missing-env`. Execute mode also blocks provider-backed steps until the selected
provider is ready.

The SDK keeps three files separate:

| File | Purpose |
| --- | --- |
| `recipe.yaml` | Defines workflow metadata and ordered steps. |
| `recipes.config.yaml` | Defines runner policy: recipe search paths, write roots, review policy, run manifest location, and the path to generation config. |
| `generation.config.yaml` | Defines provider names, model names, endpoints, and API-key environment variable names for LLM-backed steps. |

Do not put provider secrets in any of these files. Store API key values in
environment variables.

## Minimal Recipe

```yaml
schema: https://opendataproducts.org/odpr-v1.0/schema/odpr.yaml
version: "1.0"
kind: Recipe
recipe:
  metadata:
    id: RCP-CI-001
    name:
      en: Validate Catalog
  version: "1.0.0"
  type: ci
  steps:
    - id: validate-catalog
      command: validate
      with:
        document: generated/catalog.yaml
```

Validate the recipe before planning or execution:

```bash
open-data-products recipe validate recipes/ci-validate.yaml --json
```

## Runner Config

Copy the bundled recipe runner config and edit it in your project:

```bash
open-data-products config recipes --copy-to recipes.config.yaml
open-data-products config recipes --config recipes.config.yaml --check --json
```

Example:

```yaml
version: "1.0"
projectRoot: .

recipes:
  paths:
    - recipes/
    - .odp/recipes/
  defaultRecipe: recipes/release-portfolio-review.yaml

providers:
  generationConfig: generation.config.yaml
  defaultProviderRef: claude

execution:
  manifestDir: .odp/runs/
  allowWrites:
    - generated/
    - portfolio/
  requireReviewFor:
    - production
    - release
  stopOnWarning: false
```

`recipes.config.yaml` is not the LLM provider config. It only points to
`generation.config.yaml` so recipe dry-runs can resolve provider readiness.

`projectRoot` tells the runner where workflow paths are resolved from. If it is
omitted, the config file's directory is used. This keeps existing configs
working. When the config lives in a subfolder, use `projectRoot` to point back
to the project root:

```yaml
version: "1.0"
projectRoot: ..

recipes:
  paths:
    - workflows/

providers:
  generationConfig: config/generation.config.yaml

execution:
  allowWrites:
    - workspace/
```

`recipes.defaultRecipe` is a fallback for `recipe validate` and `recipe run`.
If the command includes an explicit recipe path, the command argument wins. If
the command omits a recipe path, the runner uses `recipes.defaultRecipe`. If
both are missing, the command fails with a clear error.

The Python helpers follow the same rule. `validate_recipe(config_path=...)`,
`plan_recipe_run(config_path=...)`, and `execute_recipe_run(config_path=...)`
use `recipes.defaultRecipe` when the recipe path argument is omitted, and their
JSON-compatible payloads include `recipeSelection` for the same reason as the
CLI output.

## Generation Config

Provider entries stay in `generation.config.yaml`:

```yaml
provider: claude
providers:
  claude:
    type: anthropic
    model: claude-sonnet-4-5
    apiKeyEnv: ANTHROPIC_API_KEY
```

Set the environment variable before running LLM-backed workflows:

```bash
export ANTHROPIC_API_KEY="..."
```

For local providers such as Ollama, no API-key environment variable is required:

```yaml
provider: ollama
providers:
  ollama:
    type: ollama
    model: qwen2.5
    baseUrl: http://localhost:11434
```

## Discover Recipes

List recipes from the configured search paths:

```bash
open-data-products recipe list --config recipes.config.yaml --json
```

Build a metadata-only ODPR `RecipeCatalog`:

```bash
open-data-products recipe catalog \
  --config recipes.config.yaml \
  --output recipes/catalog.yaml \
  --json
```

Search bundled ODPR recipe guidance records:

```bash
open-data-products recipe search localization --json
open-data-products recipe search --id RecipeCatalog --json
```

## Dry-Run First

Dry-run is the main agent planning surface. It validates the recipe, resolves
step parameters, checks planned writes, resolves provider readiness, and marks
review requirements. It does not call providers or write workflow outputs.

```bash
open-data-products recipe run recipes/release-portfolio-review.yaml \
  --config recipes.config.yaml \
  --dry-run \
  --json
```

Important JSON fields:

```json
{
  "mode": "dry-run",
  "recipeSelection": {
    "source": "argument",
    "path": "recipes/release-portfolio-review.yaml",
    "defaultRecipe": "recipes/ci-validate-catalog.yaml"
  },
  "canRun": true,
  "blockingReasons": [],
  "providers": [
    {
      "ref": "claude",
      "model": "claude-sonnet-4-5",
      "type": "anthropic",
      "readiness": "missing-env",
      "missingEnv": ["ANTHROPIC_API_KEY"]
    }
  ],
  "steps": [
    {
      "id": "localize",
      "command": "portfolio.localize",
      "classification": "llm-backed",
      "resolved": {
        "action": "portfolio.localize",
        "parameters": {
          "workspace": "generated/portfolio/",
          "languages": ["fi", "sv"],
          "providerRef": "claude",
          "model": "claude-sonnet-4-5"
        }
      },
      "plannedWrites": [
        {"path": "generated/portfolio/portfolio-i18n.yaml", "allowed": true},
        {"path": "generated/portfolio/index.html", "allowed": true},
        {"path": "generated/portfolio/index.fi.html", "allowed": true},
        {"path": "generated/portfolio/index.sv.html", "allowed": true}
      ],
      "review": {
        "status": "review-needed",
        "reasons": [
          {"code": "llm_backed_step"}
        ]
      }
    }
  ]
}
```

Provider readiness values:

| Value | Meaning |
| --- | --- |
| `ready` | Provider is known and any required API-key environment variables are present. |
| `missing-env` | Provider is known, but one or more required environment variables are missing. |
| `unknown-provider` | The recipe references a provider not found in generation config or built-in presets. |

`canRun` only means the recipe passed validation and write-policy checks. It
does not mean LLM-backed execution is enabled.

## Guarded Execute

Execution must be explicit:

```bash
open-data-products recipe run recipes/ci-validate.yaml \
  --config recipes.config.yaml \
  --execute \
  --json
```

LLM and review gates are separate. A command can be allowed to call an LLM only
after an explicit LLM permission flag, and a review-needed step can run only
after an explicit review approval flag:

```bash
open-data-products recipe run recipes/release-portfolio-review.yaml \
  --config recipes.config.yaml \
  --execute \
  --allow-llm \
  --approve-review \
  --json
```

Use `--allow-llm` to permit provider calls. Use `--approve-review` only after
the dry-run has been reviewed and approved. If an LLM-backed step is also
review-needed, both flags are required.

The current guarded executor runs deterministic and report-only commands such
as:

- `validate`
- `explain`
- `odpg.render`
- `portfolio.sync`
- `portfolio.render`
- `portfolio.explain`

LLM-backed commands pass the policy gates only when `--allow-llm` is set.
Commands marked `review-needed` also require `--approve-review`. Execute mode
also blocks LLM-backed steps when provider readiness is not `ready`.

The implemented LLM-backed recipe commands are:

- `generate`
- `odpg.build`
- `portfolio.build`
- `portfolio.localize`
- `portfolio.refresh`

`generate` maps to the SDK generation workflow and requires:

```yaml
with:
  input: source_docs/
  kind: signal
  output: fragments/
```

The output is usually a directory. In run manifests, `writeCheck` treats files
created inside that planned output directory as matching artifacts.

`odpg.build` maps to graph edge inference and writes graph YAML plus optional
TOON and GCF context sidecars:

```yaml
with:
  input: graph-fragments/
  output: generated/graph.yaml
  toon: generated/graph.toon
  gcf: generated/graph.gcf
```

`portfolio.build` maps to the portfolio build workflow and uses `output` for
the workspace to create:

```yaml
with:
  output: generated/portfolio/
  objectives:
    - source-lanes/objectives/
  useCases:
    - source-lanes/use-cases/
  signals:
    - source-lanes/signals/
  products:
    - source-lanes/products/
```

`portfolio.refresh` maps to the portfolio refresh workflow and uses `workspace`
for the workspace to update:

```yaml
with:
  workspace: generated/portfolio/
  objectives:
    - source-lanes/objectives/
  useCases:
    - source-lanes/use-cases/
  signals:
    - source-lanes/signals/
  products:
    - source-lanes/products/
```

It uses saved source lane paths from the portfolio workspace unless optional
lane overrides are supplied. Set `allSources: true` when the refresh should
process all saved sources instead of only new or changed source documents.

Exit codes are intentionally simple:

| Command | Exit code | Meaning |
| --- | ---: | --- |
| `recipe validate ...` | `0` | The recipe, provider, or catalog is valid. |
| `recipe validate ...` | `1` | Validation failed. |
| `recipe run ... --dry-run` | `0` | The resolved plan has `canRun: true`. |
| `recipe run ... --dry-run` | `1` | The resolved plan has blocking reasons. |
| `recipe run ... --execute` | `0` | Execution completed with `status: passed`. |
| `recipe run ... --execute` | `1` | Execution ended with `status: blocked` or `status: failed`. |

Successful and blocked executions write a compact run manifest under
`execution.manifestDir`, usually `.odp/runs/`. A run manifest is a JSON audit
record for one attempted recipe execution. It answers:

- which recipe was attempted;
- which config files were used;
- when the run started and completed;
- whether the run passed, failed, or was blocked;
- which steps ran or were blocked;
- which review signals, issues, and artifact paths were recorded.

**The manifest is needed because recipe execution can touch multiple SDK commands and multiple files.** 
Without one run-level record, a human reviewer, CI
job, or AI agent would have to infer what happened by scanning output folders
and command logs. That is brittle: files may already have existed, some steps
may have been skipped or blocked, and LLM-backed steps may require review even
when no output was written. The manifest gives one stable evidence packet for
the run.

**The manifest is log-like, but it is not a raw execution log.** A log is usually a
chronological stream of detailed messages, often noisy and implementation
specific. A run manifest is a stable machine-readable audit summary. It keeps
the fields that humans, CI jobs, and agents need to decide what happened and
what to inspect next.

Use the manifest when you need to:

- prove which recipe version and config were used;
- see why a run was blocked before execution;
- review which steps ran and which artifacts changed;
- preserve review status for release or production workflows;
- let agents continue from an audit record instead of guessing from the
  filesystem.

The CLI response includes `manifest.path`, which points to the manifest file:

```json
{
  "mode": "execute",
  "status": "passed",
  "manifest": {
    "path": ".odp/runs/odpr-20260619T090000Z.json"
  },
  "steps": [
    {
      "id": "validate-catalog",
      "command": "validate",
      "status": "passed",
      "review": {
        "status": "not-required",
        "reasons": []
      }
    }
  ]
}
```

The manifest file itself is stored as:

```text
<project-root>/<execution.manifestDir>/<runId>.json
```

With the default config, that means a path like:

```text
.odp/runs/odpr-20260619T090000Z.json
```

The current manifest JSON has this shape:

```json
{
  "runId": "odpr-20260619T090000Z",
  "mode": "execute",
  "status": "passed",
  "exitCode": 0,
  "startedAt": "2026-06-19T09:00:00+00:00",
  "completedAt": "2026-06-19T09:00:01+00:00",
  "executionPolicy": {
    "allowLlm": false,
    "reviewApproved": false
  },
  "recipe": {
    "path": "recipes/ci-validate.yaml",
    "id": "RCP-CI-001",
    "version": "1.0.0",
    "type": "ci",
    "name": {"en": "Validate Catalog"}
  },
  "config": {
    "recipeConfig": "recipes.config.yaml",
    "generationConfig": "generation.config.yaml"
  },
  "blockingReasons": [],
  "warnings": [],
  "steps": [
    {
      "id": "validate-catalog",
      "command": "validate",
      "classification": "deterministic",
      "status": "passed",
      "review": {
        "status": "not-required",
        "reasons": []
      },
      "startedAt": "2026-06-19T09:00:00+00:00",
      "completedAt": "2026-06-19T09:00:01+00:00",
      "artifacts": [],
      "issues": [],
      "summary": {
        "spec": "odpc",
        "kind": "Catalog",
        "valid": true,
        "path": "generated/catalog.yaml"
      }
    }
  ]
}
```

For blocked runs, `status` is `blocked`, `exitCode` is `1`,
`blockingReasons` explains why execution did not proceed, and each planned step
has `status: blocked`.

For failed deterministic steps, `status` is `failed`, `exitCode` is `1`, and
the failed step includes `issues`.

For `portfolio.localize`, the step summary also includes `localizationQa`.
These are objective coverage counters, not a subjective translation quality
score:

```json
{
  "summary": {
    "kind": "PortfolioLocalize",
    "valid": true,
    "workspace": "workspace",
    "localizationQa": {
      "sourceStringCount": 100,
      "languages": {
        "fi": {
          "translationCount": 99,
          "presentStringCount": 99,
          "changedStringCount": 94,
          "unchangedStringCount": 5,
          "missingStringCount": 1,
          "coverage": 0.99,
          "changedCoverage": 0.94
        }
      }
    }
  }
}
```

Executed steps that have planned writes or artifacts also include `writeCheck`.
This compares dry-run `plannedWrites` with the artifacts recorded after
execution:

```json
{
  "summary": {
    "writeCheck": {
      "status": "matched",
      "planned": [
        "workspace/portfolio-i18n.yaml",
        "workspace/index.html",
        "workspace/index.fi.html",
        "workspace/index.sv.html"
      ],
      "artifacts": [
        "workspace/portfolio-i18n.yaml",
        "workspace/index.html",
        "workspace/index.fi.html",
        "workspace/index.sv.html"
      ],
      "matched": [
        "workspace/portfolio-i18n.yaml",
        "workspace/index.html",
        "workspace/index.fi.html",
        "workspace/index.sv.html"
      ],
      "missing": [],
      "extra": []
    }
  }
}
```

`writeCheck.status` is `matched`, `missing`, `extra`, or `mismatch`. It is a
review signal; it does not turn a successful command into a failed command.

The manifest is intentionally a reference and audit record, not a copy of all
workflow outputs. It does not embed full ODPS, ODPC, ODPG, portfolio, prompt, or
generated document bodies. Use the `artifacts` paths and `summary` metadata to
decide what to inspect next.

## Write Policy

`execution.allowWrites` controls where state-changing steps may write. If the
recipe plans an output outside those roots, dry-run and execute both block the
run.

```yaml
execution:
  allowWrites:
    - generated/
    - portfolio/
```

For example, `portfolio.sync` treats its workspace as a planned write. If the
workspace is `portfolio/` but `allowWrites` only contains `generated/`, the run
is blocked before the command executes.

## Review Policy

Dry-runs and run manifests include `steps[].review.status`.

Review is marked `review-needed` when:

- the recipe has `review.required: true`;
- the recipe type is listed in `execution.requireReviewFor`;
- the step is LLM-backed.

Review status is currently advisory for deterministic/report execution. It is
still included so humans, CI jobs, and AI agents can make approval decisions
before publishing or continuing a workflow.

When execute mode is run with `--approve-review`, step results and the run
manifest record `review.decision: approved-by-cli-flag`. This records that the
runner was explicitly instructed to proceed; it is not a substitute for the
review itself.

## Agent Checklist

Agents should use this order:

1. `open-data-products recipe validate <recipe> --json`
2. `open-data-products recipe run <recipe> --config recipes.config.yaml --dry-run --json`
3. Inspect `recipeSelection`, `canRun`, `blockingReasons`, `providers`,
   `steps[].plannedWrites`, and `steps[].review`.
4. Run `--execute --json` only when the dry-run has no blocking reasons and
   the intended step classes are supported.
5. Read `manifest.path` for the audit result instead of scanning generated
   output folders directly.

MCP agents can use the safe read-only tools before handing execution to the CLI
or Python API:

- `list_recipes`
- `search_recipe_guidance`
- `validate_recipe`
- `plan_recipe_run`

The MCP server does not execute recipes. Execute mode can write manifests and
artifacts, so it remains a CLI/Python operation.
