# What Python tools are available for ODPV?

The ODPV source repository includes Python tools for validating the vocabulary, generating derived vocabulary artifacts, and searching vocabulary terms.

These tools make ODPV practical for metadata validation, documentation generation, AI-assisted discovery, and GraphRAG-ready vocabulary workflows.

## Where are the tools?

The tools live in the official ODPV repository:

https://github.com/Open-Data-Product-Initiative/odpv-v1.0/tree/main/scripts

## Validate the vocabulary

Use `validate_vocab.py` to validate the canonical ODPV vocabulary and check that derived artifacts are in sync.

```bash
python scripts/validate_vocab.py
```

The script validates the vocabulary structure, compares generated artifacts, checks `odpv.json` against `odpv.yaml`, verifies `terms.jsonl`, and confirms section files match the canonical vocabulary.

## Generate derived vocabulary artifacts

Use `generate_vocab_artifacts.py` to regenerate derived vocabulary outputs from the canonical vocabulary.

```bash
python scripts/generate_vocab_artifacts.py
python scripts/generate_vocab_artifacts.py --check
```

The `--check` option is useful in CI because it reports out-of-sync artifacts without writing files.

## Search vocabulary terms

Use `search_vocab.py` to find ODPV terms by keyword.

```bash
python scripts/search_vocab.py "data quality"
python scripts/search_vocab.py "supports" --limit 10
python scripts/search_vocab.py "business objective" --json
```

The search tool scores matches across fields such as term ID, preferred label, aliases, definition, examples, related terms, and section.

## Shared utility module

The ODPV scripts also use `vocab_utils.py`, which contains shared helpers for loading the canonical vocabulary, iterating terms, validating data, and building generated artifacts.

## Summary

Use the ODPV Python tools when you need to validate vocabulary changes, regenerate derived vocabulary files, or search controlled vocabulary terms for catalogs, graphs, agents, and documentation.

[BACK TO INDEX](https://github.com/Open-Data-Product-Initiative/odps-examples/blob/main/README.md)
