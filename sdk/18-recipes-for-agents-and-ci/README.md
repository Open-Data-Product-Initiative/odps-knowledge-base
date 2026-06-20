# Guide 18: Recipes For Agents And CI

Recipes are useful for people, but they are especially important for AI agents
and CI jobs. They expose workflow intent before execution and write manifests
after execution.

## 1. Agent-Safe Order Of Operations

An AI agent should follow this order:

1. Validate the recipe.
2. Dry-run the recipe with JSON output.
3. Check `canRun`, `blockingReasons`, provider readiness, inputs, planned
   writes, and review status.
4. Execute only when policy allows it.
5. Read the manifest instead of guessing from output folders.

## 2. CI Pattern

Use deterministic recipes for CI:

```bash
repo="$(pwd)"
tmpdir="$(mktemp -d)"
cp -R "$repo/sdk/recipes" "$tmpdir/recipes"
cd "$tmpdir/recipes"

open-data-products recipe validate \
  workflows/ci-validate-catalog.yaml \
  --json

open-data-products recipe run \
  workflows/ci-validate-catalog.yaml \
  --config config/recipes.config.yaml \
  --execute \
  --json
```

The temporary copy keeps `.odp/runs` and any generated files out of the
repository checkout. CI should usually avoid hosted LLM calls unless the
project explicitly permits them.

## 3. Agent Pattern

Use dry-run JSON as the agent contract:

```bash
open-data-products recipe run \
  sdk/recipes/workflows/portfolio-build.yaml \
  --config sdk/recipes/config/recipes.config.yaml \
  --dry-run \
  --json
```

The agent should not infer hidden behavior from prose. It should use the
structured fields in the dry-run response.

## 4. What You Can Do Now

You can now use the SDK to:

- validate and explain standards files;
- configure local and hosted LLM providers;
- generate ODPS drafts and ODPC fragments;
- build ODPG graphs;
- build, refresh, sync, localize, render, and explain portfolio workspaces;
- define repeatable ODPR recipe workflows;
- inspect run manifests for audit evidence.

## 5. References

- [Knowledge base README](../../README.md)
- [SDK guide index](../README.md)
- [Recipe examples](../recipes/)
- [ODPR recipe workflows reference](../recipe-workflows-reference.md)
- [Configure LLMs with a local config file](../11-configure-llms-with-local-config-file/)
- [ODPS product specification](https://opendataproducts.org/v4.1/)
- [ODPC catalog specification](https://opendataproducts.org/odpc-v1.0/)
- [ODPG graph specification](https://opendataproducts.org/odpg-v1.0/)
- [ODPV vocabulary specification](https://opendataproducts.org/odpv-v1.0/)
- [ODPR recipe specification](https://opendataproducts.org/odpr-v1.0/)

## What You Learned

- Recipes make SDK workflows repeatable.
- Dry-run JSON is the safe planning surface.
- Execution manifests are the audit surface.
- Human review remains required for draft LLM-generated artifacts.
