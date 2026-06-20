# Guide 17: Portfolio Recipes End To End

Portfolio recipes turn source lane notes into a reviewable workspace, update
that workspace later, and localize the rendered HTML for release review.

## Before You Run This

Use a temporary copy so generated artifacts do not modify the repository:

```bash
repo="$(pwd)"
tmpdir="$(mktemp -d)"
cp -R "$repo/sdk/recipes" "$tmpdir/recipes"
cd "$tmpdir/recipes"
```

Set a hosted provider key if you plan to execute the LLM-backed examples:

```bash
export ANTHROPIC_API_KEY="your-key"
```

## 1. Build A Portfolio Workspace

Dry-run first:

```bash
open-data-products recipe run workflows/portfolio-build.yaml \
  --config config/recipes.config.yaml \
  --dry-run \
  --json
```

Execute only after the dry-run plan is clean and reviewed:

```bash
open-data-products recipe run workflows/portfolio-build.yaml \
  --config config/recipes.config.yaml \
  --execute \
  --allow-llm \
  --approve-review \
  --json
```

Inspect the workspace:

```bash
find workspace -maxdepth 3 -type f | sort
sed -n '1,180p' workspace/portfolio.yaml
```

## 2. Refresh The Workspace

Dry-run first:

```bash
open-data-products recipe run workflows/portfolio-refresh.yaml \
  --config config/recipes.config.yaml \
  --dry-run \
  --json
```

Execute only after the dry-run plan is clean and reviewed:

```bash
open-data-products recipe run workflows/portfolio-refresh.yaml \
  --config config/recipes.config.yaml \
  --execute \
  --allow-llm \
  --approve-review \
  --json
```

Refresh is useful when source lane notes change and the workspace already
exists.

## 3. Localize The Release View

Dry-run first:

```bash
open-data-products recipe run workflows/release-portfolio-localize.yaml \
  --config config/recipes.config.yaml \
  --dry-run \
  --json
```

Execute only after the dry-run plan is clean and reviewed:

```bash
open-data-products recipe run workflows/release-portfolio-localize.yaml \
  --config config/recipes.config.yaml \
  --execute \
  --allow-llm \
  --approve-review \
  --json
```

Localization writes translated HTML pages while keeping canonical YAML in the
default language.

## 4. Inspect QA And Write Checks

```bash
python3 - <<'PY'
import json
from pathlib import Path

for manifest in sorted(Path(".odp/runs").glob("*.json")):
    data = json.loads(manifest.read_text())
    print(manifest, data["status"], data["exitCode"])
    for step in data["steps"]:
        summary = step.get("summary", {})
        print(step["command"], summary.get("writeCheck", {}).get("status"))
        if "localizationQa" in summary:
            print(json.dumps(summary["localizationQa"], indent=2))
PY
```

Generated artifacts are drafts. Review the HTML, YAML, manifests, and warnings
before using the output in a release.

## What You Learned

- `portfolio.build` creates a workspace from source lanes.
- `portfolio.refresh` updates an existing workspace.
- `portfolio.localize` creates localized review pages.
- Manifests provide audit evidence for generated artifacts.

## Next Guide

Continue to [Guide 18: Recipes For Agents And CI](../18-recipes-for-agents-and-ci/).
