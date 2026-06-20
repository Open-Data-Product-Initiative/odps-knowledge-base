# Guide 12: Why Recipes Matter And What They Run

So far, you have learned individual SDK commands. You can validate files,
generate fragments, build graphs, build portfolios, refresh them, localize
them, and explain the result.

That is powerful, but real work is rarely one command. A release workflow might
need five or six steps, the right provider, the right model, the right folders,
review approval, and a record of what changed. If every person or AI agent
rebuilds that sequence from memory, the workflow becomes fragile.

Recipes solve that problem by turning SDK command sequences into named,
reviewable workflows. Instead of copying commands between terminals, notebooks,
CI jobs, and agent prompts, a project can store the workflow as an ODPR recipe
file and run it the same way each time.

## Why This Matters For Business

Recipe workflows matter because data product work is repeated business work,
not a one-time technical experiment. Teams need to refresh portfolios when
source material changes, validate release artifacts, generate graphs, localize
review pages, and keep evidence of what was done.

Without recipes, the process depends on people remembering the right command
sequence. That creates practical risks:

- different people run slightly different workflows;
- LLM-backed steps happen without a clear review gate;
- generated files appear without a manifest explaining where they came from;
- CI jobs and AI agents have to guess what should happen;
- release reviews depend on terminal history instead of committed workflow
  definitions.

With recipes, the workflow becomes explicit. A team can review the workflow
before running it, automate it safely, and keep a manifest after execution.

## What Is In It For You

Recipes help you as a developer, data product owner, reviewer, or AI-agent user:

- you can run a complete workflow with one recipe command;
- you can dry-run before execution and see inputs, planned writes, provider
  readiness, and review requirements;
- you can separate workflow policy from provider credentials;
- you can make CI jobs repeat the same checks every time;
- you can give AI agents a structured plan instead of asking them to infer
  steps from prose;
- you can keep run manifests as audit evidence.

The practical payoff is consistency. The same workflow can be used locally,
inside CI, in a course exercise, or by an AI agent.

## What A Recipe Is

A recipe is a YAML document that describes a repeatable SDK workflow. It does
not contain the generated portfolio, graph, catalog, or product body. Instead,
it describes the steps that should create, check, update, or explain those
artifacts.

A recipe usually answers these questions:

- What workflow are we running?
- Which SDK commands are part of it?
- What files or folders does each step read?
- What files or folders may each step write?
- Does a step call an LLM provider?
- Does the workflow require human review before execution?

That makes the recipe readable as documentation and executable as
configuration.

## Before You Run This

Install the SDK and run the commands from the repository root if you are using
the cloned examples:

```bash
pip install open-data-products
```

The starter recipe files live under:

```text
sdk/recipes/
```

## 1. From Commands To Workflow

Direct SDK commands are still useful:

```bash
open-data-products validate sdk/recipes/workspace/odpc/catalog.yaml
open-data-products portfolio explain sdk/recipes/workspace/
```

A recipe adds the workflow layer around those commands:

- workflow metadata and purpose;
- ordered steps;
- provider and model choices for LLM-backed steps;
- declared inputs and planned writes;
- review policy;
- dry-run output for humans, CI, and AI agents;
- execution manifests under `.odp/runs/`.

For example, a release workflow can say: localize this portfolio, use this
provider, require review approval, write only inside the allowed workspace, and
record the run manifest.

## 2. Starter Recipe Files

Inspect the starter workflows:

```bash
find sdk/recipes/workflows -maxdepth 1 -type f -name "*.yaml" | sort
```

You should see examples for validation, signal generation, graph build,
portfolio build, portfolio refresh, portfolio sync/render/explain, and
localization.

## 3. Recipe Files Versus Config Files

Recipes describe what should run. Config files describe how the runner behaves.

```text
sdk/recipes/workflows/*.yaml       # workflow definitions
sdk/recipes/config/recipes.config.yaml
sdk/recipes/config/generation.config.yaml
```

Keep that split clear:

- the recipe owns the workflow steps;
- `recipes.config.yaml` owns runner policy;
- `generation.config.yaml` owns LLM provider settings.

## 4. The New Operating Model

The new operating model is simple:

1. Define the workflow as a recipe.
2. Validate the recipe.
3. Dry-run the recipe and inspect the plan.
4. Execute only when inputs, planned writes, provider readiness, and review
   status are acceptable.
5. Read the manifest after execution.

This is why recipes are useful for both humans and AI agents. The workflow is
not hidden in a tutorial, shell history, or agent prompt. It is an executable
file with a dry-run plan and a run manifest.

## What You Learned

- Recipes are workflow contracts around existing SDK commands.
- Recipes solve repeatability, review, audit, and automation problems.
- Recipes do not replace direct CLI commands.
- Runner config and generation config are separate from the recipe file.
- The next step is to validate, list, and dry-run recipes before executing
  anything.

## Next Guide

Continue to [Guide 13: Validate, List, And Dry-Run Recipes](../13-validate-list-and-dry-run-recipes/).
