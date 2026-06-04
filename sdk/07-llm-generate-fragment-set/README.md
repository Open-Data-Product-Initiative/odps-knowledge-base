# Guide 7: Generate a Full Fragment Set from Source Documents

This guide uses local Ollama/Qwen 2.5 to generate multiple ODPC fragments from
type-specific source folders.

## 1. Open this guide folder and prepare output

```bash
cd sdk/07-llm-generate-fragment-set
mkdir -p fragments
```

This folder already contains the source documents under type-specific folders:

```text
source_docs/products/
source_docs/use_cases/
source_docs/objectives/
source_docs/signals/
```

If you want to recreate the source files yourself, replace them with:

```bash
cat > source_docs/products/airport-operations-product.md <<'MD'
# Airport Operations Performance Product

This data product combines flight schedule, gate assignment, turnaround status,
crew readiness, and departure delay information. It supports operational
decision making in the airport operations control center.
MD

cat > source_docs/use_cases/delay-risk-use-case.md <<'MD'
# Delay Risk Monitoring Use Case

Operations controllers need to identify flights at risk of delayed departure
at least 20 minutes before scheduled off-block time. The use case supports
prioritizing recovery actions for crews, gates, baggage, and cleaning.
MD

cat > source_docs/objectives/reduce-delay-objective.txt <<'TXT'
Business objective: reduce average departure delay minutes for short-haul
flights during morning and evening peak periods. The objective is measured by
delay minutes, number of recovered flights, and operational response time.
TXT

cat > source_docs/signals/turnaround-delay-signal.txt <<'TXT'
Signal: turnaround delay risk increases when inbound arrival is late, baggage
unloading has not started, cleaning crew is not assigned, or the gate has a
conflict with another aircraft movement.
TXT
```

## 3. Generate product fragments

```bash
open-data-products generate \
  --input source_docs/products/ \
  --kind product-reference \
  --output fragments/ \
  --json

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

## 4. Inspect generated artifacts

```bash
ls fragments/
```

Expected artifact types:

- `product_reference_*.yaml`
- `use_case_*.yaml`
- `business_objective_*.yaml`
- `signal_*.yaml`

## 5. Build and validate a catalog

```bash
open-data-products odpc-build fragments/ \
  --output catalog.yaml \
  --json

open-data-products validate catalog.yaml --json
```

## What You Learned

- Type-specific folder input keeps each selected prompt focused.
- Generated fragments are separate YAML files.
- The generated ODPC fragments can be collected into a catalog.

## Next Guide

Continue to [Guide 8: Full Cycle from Source Docs to Catalog and Graph HTML](../08-llm-full-cycle-catalog-and-graph/).
