# Guide 15: Run Deterministic Recipes

Deterministic recipes do not call an LLM. They are the safest recipes to run
first because they validate, sync, render, or explain existing artifacts.

## Before You Run This

The deterministic examples are:

```text
sdk/recipes/workflows/ci-validate-catalog.yaml
sdk/recipes/workflows/portfolio-sync-render.yaml
```

Use a temporary copy so run manifests and rendered files do not modify the
repository:

```bash
repo="$(pwd)"
tmpdir="$(mktemp -d)"
cp -R "$repo/sdk/recipes" "$tmpdir/recipes"
cd "$tmpdir/recipes"
```

## 1. Execute Catalog Validation

Run the CI validation recipe:

```bash
open-data-products recipe run \
  workflows/ci-validate-catalog.yaml \
  --config config/recipes.config.yaml \
  --execute \
  --json
```

This validates the example ODPC catalog and writes a compact run manifest.

## 2. Execute Portfolio Sync, Render, And Explain

Run the deterministic portfolio recipe:

```bash
open-data-products recipe run \
  workflows/portfolio-sync-render.yaml \
  --config config/recipes.config.yaml \
  --execute \
  --json
```

This recipe updates the example workspace, renders HTML, and summarizes the
portfolio without calling a provider.

## 3. Inspect The Run Manifest

Open the most recent manifest:

```bash
python3 - <<'PY'
import json
from pathlib import Path

manifest = sorted(Path(".odp/runs").glob("*.json"))[-1]
data = json.loads(manifest.read_text())

print(manifest)
print(data["status"], data["exitCode"])
for step in data["steps"]:
    print(step["id"], step["command"], step["status"])
    print(json.dumps(step.get("summary", {}), indent=2))
PY
```

When you are done, remove the temp folder if you want:

```bash
cd "$repo"
rm -rf "$tmpdir"
```

## What You Learned

- Deterministic recipes can execute without provider keys.
- Run manifests record status, steps, artifacts, and summaries.
- `writeCheck` compares planned writes with actual artifacts when writes occur.

## Next Guide

Continue to [Guide 16: Run LLM-Backed Recipes](../16-run-llm-backed-recipes/).
