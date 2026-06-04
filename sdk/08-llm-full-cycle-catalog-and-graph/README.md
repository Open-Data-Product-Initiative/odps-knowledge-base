# Guide 8: Full Cycle from Source Docs to Catalog and Graph HTML

This guide shows the complete LLM-assisted flow:

1. Put `.md` and `.txt` source files into type-specific source directories.
2. Generate ODPC fragments.
3. Build an ODPC catalog YAML file.
4. Build an ODPC catalog HTML page.
5. Build an ODPG graph from the same fragments.
6. Generate an ODPG graph explorer HTML page.

## 1. Open this guide folder and prepare folders

```bash
cd sdk/08-llm-full-cycle-catalog-and-graph
mkdir -p source_docs/products
mkdir -p source_docs/use_cases
mkdir -p source_docs/objectives
mkdir -p source_docs/signals
mkdir -p fragments output
```

## 2. Add source documents

Use a mix of Markdown and text files. Keep each artifact type in its own folder
so the selected `--kind` prompt only sees matching source material.

```bash
cat > source_docs/products/airport-operations-product.md <<'MD'
# Airport Operations Performance Product

The product provides a trusted operational view of flights, gates, turnaround
milestones, baggage status, cleaning readiness, and delay risk. Primary users
are airport operations controllers and airline station managers.
MD

cat > source_docs/products/passenger-flow-product.md <<'MD'
# Passenger Flow Queue Product

The product combines security wait time, passenger count, checkpoint capacity,
and boarding gate demand. It helps terminal operations prevent queue congestion
and missed connections.
MD

cat > source_docs/use_cases/delay-risk-use-case.md <<'MD'
# Flight Delay Risk Monitoring

Operations teams need to detect flights likely to miss scheduled departure.
The use case supports early intervention for gate conflicts, turnaround tasks,
crew readiness, and baggage loading.
MD

cat > source_docs/use_cases/connection-protection-use-case.md <<'MD'
# Passenger Connection Protection

The airport wants to identify inbound passengers at risk of missing outbound
connections. The use case supports gate coordination, passenger assistance,
and proactive disruption management.
MD

cat > source_docs/objectives/reduce-delay-objective.txt <<'TXT'
Objective: reduce average departure delay minutes and improve recovered flight
count during peak operating windows. Success is measured by delay minutes,
recovery actions completed, and passenger connection success rate.
TXT

cat > source_docs/signals/turnaround-delay-signal.txt <<'TXT'
Signal: turnaround delay risk rises when inbound arrival is late, unloading has
not started, cleaning crew is missing, fueling is delayed, or a gate conflict
exists.
TXT

cat > source_docs/signals/security-queue-signal.txt <<'TXT'
Signal: security queue surge risk rises when passenger volume exceeds planned
checkpoint capacity and estimated wait time crosses the operating threshold.
TXT
```

## 3. Generate product fragments

This command uses the default local provider, Ollama with Qwen 2.5:

```bash
open-data-products generate \
  --input source_docs/products/ \
  --kind product-reference \
  --output fragments/ \
  --json
```

Generate the other ODPC fragments from their matching source folders:

```bash
open-data-products generate \
  --input source_docs/use_cases/ \
  --kind use-case \
  --output fragments/ \
  --json

open-data-products generate \
  --input source_docs/objectives/ \
  --kind objective \
  --output fragments/ \
  --json

open-data-products generate \
  --input source_docs/signals/ \
  --kind signal \
  --output fragments/ \
  --json
```

## 4. Build the ODPC catalog YAML and HTML

```bash
open-data-products odpc-build fragments/ \
  --output output/catalog.yaml \
  --html output/catalog.html \
  --json
```

Open `output/catalog.html` in a browser to inspect the human-friendly catalog.

## 5. Build and validate the ODPG graph

```bash
open-data-products odpg-build fragments/ \
  --output output/graph.yaml \
  --json

open-data-products validate output/graph.yaml --json
```

Fix source text or rerun generation if validation fails.

## 6. Generate the ODPG graph explorer

```bash
open-data-products odpg-generate output/graph.yaml \
  --output output/graph-explorer.html \
  --json
```

Open `output/graph-explorer.html` in a browser to explore the generated graph.

## 7. Optional checks

```bash
open-data-products odpc-summary output/catalog.yaml --json
open-data-products odpg-summary output/graph.yaml
```

## What You Learned

- Source documents can be plain `.md` and `.txt` files.
- Type-specific source folders keep each selected `--kind` prompt focused.
- Generation creates separate ODPC fragment files, not one large mixed file.
- The generated fragments can become an ODPC catalog.
- The same generated fragments can become an ODPG graph and interactive HTML
  explorer.

## Next Guide

Continue to [Guide 9: Build Catalog and Graph from the Same Fragments with Claude](../09-build-catalog-and-graph-from-fragments/).
