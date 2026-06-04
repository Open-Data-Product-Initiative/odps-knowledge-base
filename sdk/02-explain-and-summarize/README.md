# Guide 2: Explain and Summarize a Product

This guide uses the included `product.yaml` sample and shows how to inspect the
document without reading every line manually.

## 1. Open this guide folder

```bash
cd sdk/02-explain-and-summarize
```

The folder includes the same simple ODPS product used in Guide 1. Confirm it is
valid before inspecting it:

```bash
open-data-products validate product.yaml
```

## 2. Explain the document

```bash
open-data-products explain product.yaml
```

The explanation is compact and intended for humans, agents, and automation
logs.

## 3. Get the explanation as JSON

```bash
open-data-products explain product.yaml --json
```

Use this form when another system needs to read the result.

## 4. Load a lightweight summary

```bash
open-data-products summary product.yaml
```

Summary output gives file-level metadata such as detected spec, kind, size,
and hash. It does not return the full document body.

## 5. List references

```bash
open-data-products refs product.yaml --json
```

For this simple product there may be no references. In larger ODPS, ODPC, and
ODPG files, this helps discover linked artifacts.

## What You Learned

- `explain` gives a readable document overview.
- `summary` gives lightweight metadata without loading the body into output.
- `refs` helps discover `$ref` and `ref` links.

## Next Guide

Continue to [Guide 3: Use the ODPV Vocabulary Helpers](../03-use-vocabulary-helpers/).
