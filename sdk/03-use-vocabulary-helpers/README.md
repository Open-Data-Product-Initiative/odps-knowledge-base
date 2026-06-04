# Guide 3: Use the ODPV Vocabulary Helpers

The SDK includes Open Data Product Vocabulary helpers. These are useful when
you want to use standard terms consistently.

## 1. Summarize the vocabulary

```bash
open-data-products odpv-summary --json
```

This returns vocabulary sections and term counts.

## 2. Search by keyword

```bash
open-data-products odpv-search "governance policy risk" --limit 3 --json
```

Search helps you find the right vocabulary term when you do not know the exact
term id.

## 3. Resolve a phrase to a canonical term

```bash
open-data-products odpv-resolve "reusable data asset" --json
```

The resolver can match aliases and plain-language text to a standard term.

## 4. Explain one term

```bash
open-data-products odpv-explain DataProduct --json
```

This returns the canonical vocabulary packet for `DataProduct`.

## 5. Check a relationship

```bash
open-data-products odpv-relationship DataProduct supports UseCase --json
```

This checks whether the relationship makes sense for the selected source and
target types.

## What You Learned

- ODPV commands help humans use shared terminology.
- Search and resolve are good starting points.
- Relationship checks help avoid inconsistent graph language.

## Next Guide

Continue to [Guide 4: Convert GraphML to ODPG and Open an Explorer](../04-convert-graph-to-odpg/).
