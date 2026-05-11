# What Python tools are available for ODPC?

The ODPC source repository includes Python tools for validating catalogs, generating derived artifacts, searching catalog object records, explaining catalog files, and checking agent-friendly artifacts.

These tools are useful when you want to work with ODPC as machine-readable metadata, not only as documentation.

## Where are the tools?

The tools live in the official ODPC repository:

https://github.com/Open-Data-Product-Initiative/odpc-v1.0/tree/main/scripts

## Install dependencies

From a local clone of the ODPC repository:

```bash
python -m pip install -r scripts/requirements-agent.txt
```

## Validate an ODPC catalog

Use `validate_catalog.py` to validate an ODPC YAML or JSON catalog against the ODPC schema.

```bash
python scripts/validate_catalog.py source/catalog/examples/full.yaml
```

The script reports whether the file is a valid ODPC catalog and prints schema validation errors when it is not.

## Explain a catalog for humans or agents

Use `explain_catalog.py` to produce a compact summary of a catalog file.

```bash
python scripts/explain_catalog.py source/catalog/examples/full.yaml
```

The output includes the catalog ID, name, status, object counts, graph reference, object IDs, and hints such as missing product references or missing graph references.

## Search ODPC object records

Use `search_objects.py` to search the agent-friendly ODPC object records in `source/catalog/objects.jsonl`.

```bash
python scripts/search_objects.py demand
python scripts/search_objects.py --id ProductReference
python scripts/search_objects.py signal --json
```

This helps humans and AI agents find the right ODPC object, required fields, use guidance, and example files.

## Generate derived catalog artifacts

Use `generate_catalog_artifacts.py` to generate derived artifacts from canonical ODPC sources.

```bash
python scripts/generate_catalog_artifacts.py
python scripts/generate_catalog_artifacts.py --check
```

The `--check` option is useful in CI because it fails when generated artifacts are out of date.

## Check agent artifacts

Use `check_agent_artifacts.py` to verify the consistency of agent-facing ODPC artifacts, examples, schema files, object records, and `llms.txt` references.

```bash
python scripts/check_agent_artifacts.py
```

## Summary

Use the ODPC Python tools when you need to validate catalog files, keep generated schema artifacts in sync, search object guidance, or prepare ODPC metadata for AI-assisted catalog and portfolio workflows.

[BACK TO INDEX](https://github.com/Open-Data-Product-Initiative/odps-examples/blob/main/README.md)
