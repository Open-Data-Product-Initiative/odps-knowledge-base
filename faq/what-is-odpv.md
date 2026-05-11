# What is ODPV, and why should I use it?

ODPV stands for **Open Data Product Vocabulary**. It is a vendor-neutral, open-source, machine-readable controlled vocabulary for data product management.

ODPV defines shared terms used across the OpenDataProducts.org standards family, including data products, catalogs, graphs, value concepts, governance concepts, and relationship terms.

## Why was ODPV created?

As data product specifications grow, terminology can drift. One system may say "data product", another may say "data offering", and a third may use "reusable data asset". ODPV gives these concepts stable reference terms.

This helps teams, tools, catalogs, graph systems, and AI assistants use the same language when describing data product portfolios.

## What ODPV defines

The first version of ODPV focuses on four concept groups:

- **ODPV Core**: foundational objects, roles, classifications, and references
- **ODPV Value**: business value, demand, outcomes, gaps, and priorities
- **ODPV Governance**: quality, access, licensing, agreements, policy, and compliance
- **ODPV Relationships**: relationship terms for graphs and portfolio analysis

## Quick example

Here is an ODPV term definition for `DataProduct`:

```yaml
id: DataProduct
uri: https://opendataproducts.org/odpv-v1.0/terms/DataProduct
type: object
status: stable
introducedIn: 1.0.0
preferredLabel:
  en: Data Product
definition:
  en: A managed data offering designed for reuse, with defined ownership, access, quality, usage terms, and value context.
alsoKnownAs:
  en:
    - data product
    - data offering
    - reusable data asset
relatedTerms:
  - Dataset
  - DataService
  - Distribution
usedIn:
  - ODPS
  - ODPC
  - ODPG
```

## Who should use ODPV?

Use ODPV when you need consistent vocabulary across specifications, catalogs, graph implementations, metadata validation, AI-assisted discovery, GraphRAG, or tool development.

Learn more in the official [ODPV source repository](https://github.com/Open-Data-Product-Initiative/odpv-v1.0).

[BACK TO INDEX](https://github.com/Open-Data-Product-Initiative/odps-examples/blob/main/README.md)
