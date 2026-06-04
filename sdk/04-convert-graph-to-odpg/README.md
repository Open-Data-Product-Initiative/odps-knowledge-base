# Guide 4: Convert GraphML to ODPG and Open an Explorer

This guide converts a small external GraphML graph into ODPG YAML, validates
the result, and creates a standalone HTML graph explorer.

## 1. Open this guide folder

```bash
cd sdk/04-convert-graph-to-odpg
```

This folder already includes `graph.graphml`, so you can run the conversion
commands immediately.

If you want to recreate the file yourself, replace `graph.graphml` with:

```bash
cat > graph.graphml <<'XML'
<graphml>
  <key id="nodeType" for="node" attr.name="type"/>
  <key id="edgeType" for="edge" attr.name="type"/>
  <graph edgedefault="directed">
    <node id="airport-operations">
      <data key="nodeType">DataProduct</data>
    </node>
    <node id="delay-risk-monitoring">
      <data key="nodeType">UseCase</data>
    </node>
    <edge source="delay-risk-monitoring" target="airport-operations">
      <data key="edgeType">uses</data>
    </edge>
  </graph>
</graphml>
XML
```

## 2. Convert GraphML to ODPG YAML

```bash
open-data-products odpg-convert \
  --input graph.graphml \
  --output graph.yaml \
  --json
```

## 3. Validate the converted graph

```bash
open-data-products validate graph.yaml --json
```

## 4. Generate a graph explorer

```bash
open-data-products odpg-generate graph.yaml --output graph-explorer.html --json
```

Open `graph-explorer.html` in a browser.

## What You Learned

- `odpg-convert` turns external graph formats into ODPG YAML.
- The converted graph can be validated like any other ODPG document.
- The same graph can be rendered as a standalone HTML explorer.

## Next Guide

Continue to [Guide 5: Generate One Signal Fragment with Ollama](../05-llm-generate-one-signal/).
