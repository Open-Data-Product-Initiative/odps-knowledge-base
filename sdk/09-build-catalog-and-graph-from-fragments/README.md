# Guide 9: Build Catalog and Graph from the Same Fragments with Claude

This guide shows how one ODPC fragment folder can produce both an ODPC catalog
and an ODPG graph using Claude for LLM-assisted generation and edge inference.

## 1. Open this guide folder and prepare output

```bash
cd sdk/09-build-catalog-and-graph-from-fragments
mkdir -p fragments output
```

This folder already contains the customer analytics and support operations
source documents under type-specific folders:

```text
source_docs/products/
source_docs/use_cases/
source_docs/objectives/
source_docs/signals/
```

If you want to recreate the source documents yourself, replace them with:

```bash
cat > source_docs/products/customer-analytics-product.md <<'MD'
# Customer Analytics Product

The product provides customer profile, purchase, support, and churn risk data
for retention teams. It is used by the Customer Retention use case and supports
the Reduce Preventable Churn objective. It consumes the Churn Risk Signal.
MD

cat > source_docs/products/support-operations-product.md <<'MD'
# Support Operations Product

The product provides support ticket volume, response time, backlog, escalation,
and customer sentiment data for service operations teams. It is used by the
Support Escalation Management use case and supports the Improve Support
Resolution objective. It consumes the Escalation Pressure Signal.
MD

cat > source_docs/use_cases/customer-retention-use-case.md <<'MD'
# Customer Retention

Retention teams need trusted customer analytics to identify customers at risk
and choose the next best action. The use case depends on the Customer Analytics
Product, monitors the Churn Risk Signal, and contributes to the Reduce
Preventable Churn objective.
MD

cat > source_docs/use_cases/support-escalation-use-case.md <<'MD'
# Support Escalation Management

Service operations teams need to identify accounts likely to escalate because
support queues are growing or response times are slipping. The use case depends
on the Support Operations Product, monitors the Escalation Pressure Signal, and
contributes to the Improve Support Resolution objective.
MD

cat > source_docs/objectives/reduce-churn-objective.txt <<'TXT'
Objective: reduce preventable churn by improving retention decision quality and
intervention timing. The Customer Retention use case and Customer Analytics
Product support this objective. Churn Risk Signal measures early warning risk.
TXT

cat > source_docs/objectives/improve-support-resolution-objective.txt <<'TXT'
Objective: improve support resolution by reducing escalation rate, backlog age,
and first response delay. The Support Escalation Management use case and Support
Operations Product support this objective. Escalation Pressure Signal measures
when the support operation is under stress.
TXT

cat > source_docs/signals/churn-risk-signal.txt <<'TXT'
Daily retention briefing from April 18, 2026 at 09:30.

The customer analytics event log shows a churn-risk pattern: product usage is
down, support tickets are up, and renewal activity has slowed for several
priority accounts. Retention teams use this daily signal inside the Customer
Analytics Product and monitor it in the Customer Retention use case. The signal
is an early warning for the Reduce Preventable Churn objective.
TXT

cat > source_docs/signals/escalation-pressure-signal.txt <<'TXT'
Support operations queue note from April 18, 2026 at 10:00.

The hourly queue monitor shows escalation pressure building: backlog is growing,
first response time is slipping, customer sentiment is dropping, and priority
accounts are waiting too long. Service operations teams use this signal inside
the Support Operations Product and monitor it in the Support Escalation
Management use case. The signal is an early warning for the Improve Support
Resolution objective.
TXT
```

## 3. Configure Claude

Claude generation uses the Anthropic API key from the environment:

```bash
export ANTHROPIC_API_KEY="your-api-key"
```

The commands below select the bundled `claude` provider and the
`claude-sonnet-4-5` model explicitly.

## 4. Generate ODPC fragments

Generate each fragment type into the same output folder, but read each type
from its own source folder:

```bash
open-data-products generate \
  --provider claude \
  --model claude-sonnet-4-5 \
  --input source_docs/products/ \
  --kind product-reference \
  --output fragments/ \
  --json

open-data-products generate \
  --provider claude \
  --model claude-sonnet-4-5 \
  --input source_docs/use_cases/ \
  --kind use-case \
  --output fragments/ \
  --json

open-data-products generate \
  --provider claude \
  --model claude-sonnet-4-5 \
  --input source_docs/objectives/ \
  --kind objective \
  --output fragments/ \
  --json

open-data-products generate \
  --provider claude \
  --model claude-sonnet-4-5 \
  --input source_docs/signals/ \
  --kind signal \
  --output fragments/ \
  --json
```

## 5. Build the ODPC catalog

```bash
open-data-products odpc-build fragments/ \
  --output output/catalog.yaml \
  --html output/catalog.html \
  --json
```

The catalog command collects the ODPC fragments into one catalog document.

## 6. Build the ODPG graph from the same fragments

```bash
open-data-products odpg-build fragments/ \
  --provider claude \
  --model claude-sonnet-4-5 \
  --output output/graph.yaml \
  --id customer-retention-graph \
  --name "Customer Retention Graph" \
  --json
```

The graph command converts the ODPC fragments into ODPG nodes and uses the
Claude provider to infer the edges between those nodes.

## 7. Validate and open the graph explorer

```bash
open-data-products validate output/graph.yaml --json

open-data-products odpg-generate output/graph.yaml \
  --output output/graph-explorer.html \
  --json
```

Open `output/graph-explorer.html` in a browser to inspect the relationships.

## What You Learned

- ODPC fragments can feed both catalog and graph workflows.
- Claude can generate the ODPC fragments and infer the ODPG graph edges.
- `odpc-build` creates one catalog from the fragment folder.
- `odpg-build` creates ODPG nodes from the same fragments and asks the LLM only
  for graph edges.
- `odpg-generate` turns the graph YAML into a browser-viewable explorer.

## Next Guide

Continue to [Guide 10: Set Up a Local LLM with Ollama and Qwen](../10-set-up-local-llm-qwen/).
