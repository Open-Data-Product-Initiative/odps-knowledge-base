# Guide 13: Validate, List, And Dry-Run Recipes

The first habit with recipes is inspection before execution. Validation checks
the recipe shape. Listing shows what workflows are available. Dry-run explains
what would happen without writing artifacts.

## Before You Run This

Run from the repository root:

```bash
pwd
```

The examples use:

```text
sdk/recipes/config/recipes.config.yaml
```

## 1. Validate A Recipe

Validate the catalog validation recipe:

```bash
open-data-products recipe validate \
  sdk/recipes/workflows/ci-validate-catalog.yaml \
  --json
```

Validation confirms the file is an ODPR `Recipe`, checks it against the bundled
schema, and reports step classification.

## 2. List Available Recipes

List recipes discovered through the runner config:

```bash
open-data-products recipe list \
  --config sdk/recipes/config/recipes.config.yaml \
  --json
```

The result is a metadata catalog. It does not execute any recipe.

## 3. Dry-Run A Recipe

Dry-run the graph build recipe:

```bash
open-data-products recipe run \
  sdk/recipes/workflows/odpg-build.yaml \
  --config sdk/recipes/config/recipes.config.yaml \
  --dry-run \
  --json
```

Look for these fields:

- `canRun`: should be `true` for a runnable plan.
- `blockingReasons`: should be empty before execution.
- `providers`: provider-backed recipes should show ready providers or explain
  missing environment variables.
- `steps[].inputs`: each required input path should exist.
- `steps[].plannedWrites`: each planned write should be allowed by policy.
- `steps[].review`: review status should be understood before execution.

Do not treat a dry-run as approval. It is the plan that tells you whether
execution is possible and what still needs human or policy approval.
For LLM-backed recipes, execution still requires provider readiness and explicit
approval flags even when dry-run can produce a plan.

## 4. Agent Reading Pattern

An AI agent should read dry-run JSON before execution:

```bash
open-data-products recipe run \
  sdk/recipes/workflows/portfolio-build.yaml \
  --config sdk/recipes/config/recipes.config.yaml \
  --dry-run \
  --json
```

The agent should verify that inputs exist, writes are allowed, provider
readiness is acceptable, and review requirements are understood.

## What You Learned

- `recipe validate` checks the recipe file.
- `recipe list` builds a recipe catalog from config.
- `recipe run --dry-run --json` is the safe planning surface.
- Dry-run JSON is the main contract for AI agents and CI.

## Next Guide

Continue to [Guide 14: Recipe Config And Execution Policy](../14-recipe-config-and-execution-policy/).
