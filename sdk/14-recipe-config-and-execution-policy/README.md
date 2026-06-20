# Guide 14: Recipe Config And Execution Policy

A recipe file does not contain every rule. Execution policy belongs in
`recipes.config.yaml`, while provider settings belong in `generation.config.yaml`.
This separation keeps workflows portable and credentials out of recipe files.

## Before You Run This

Open the two config files:

```bash
sed -n '1,220p' sdk/recipes/config/recipes.config.yaml
sed -n '1,220p' sdk/recipes/config/generation.config.yaml
```

## 1. Runner Config

`recipes.config.yaml` controls the recipe runner:

- `projectRoot`: where relative recipe paths resolve;
- `recipes.paths`: folders to scan for recipes;
- `recipes.defaultRecipe`: default path when no recipe argument is given;
- `providers.generationConfig`: provider config file to use;
- `execution.allowWrites`: write roots the recipe may change;
- `execution.manifestDir`: where run manifests are written.

## 2. Generation Config

`generation.config.yaml` controls provider details:

- provider names such as `claude` or `ollama`;
- provider type;
- model name;
- API key environment variable name;
- optional endpoint settings.

The recipe uses provider references. It does not store secrets.

## 3. Default Recipe Selection

Run the default recipe from config:

```bash
open-data-products recipe run \
  --config sdk/recipes/config/recipes.config.yaml \
  --dry-run \
  --json
```

The JSON includes `recipeSelection`. This tells a script or agent whether the
recipe came from a command argument or from config.

If both are present, the command argument wins:

```bash
open-data-products recipe run \
  sdk/recipes/workflows/portfolio-build.yaml \
  --config sdk/recipes/config/recipes.config.yaml \
  --dry-run \
  --json
```

In that case, `recipeSelection.source` is `argument`. The config default is
only used when the command does not include a recipe path.

## 4. Write Policy

Dry-run the portfolio build recipe:

```bash
open-data-products recipe run \
  sdk/recipes/workflows/portfolio-build.yaml \
  --config sdk/recipes/config/recipes.config.yaml \
  --dry-run \
  --json
```

The `plannedWrites` list shows what the workflow plans to write and whether
each path is allowed.

## What You Learned

- Recipes define steps.
- `recipes.config.yaml` defines runner policy.
- `generation.config.yaml` defines provider settings.
- `recipeSelection` and `plannedWrites` make the runner safer for automation.

## Next Guide

Continue to [Guide 15: Run Deterministic Recipes](../15-run-deterministic-recipes/).
