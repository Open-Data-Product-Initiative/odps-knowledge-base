# What is ODPC, and why should I use it?

ODPC stands for **Open Data Product Catalogs**. It is a vendor-neutral, open-source, machine-readable model for cataloging data product portfolios.

Where ODPS describes an individual data product, ODPC describes the catalog layer around many data products. It gives teams a shared way to organize product references, use cases, business objectives, signals, and catalog metadata.

## Why was ODPC created?

Data product management does not stop at one product. Organizations need to understand:

- which data products exist
- which use cases they support
- which business objectives they contribute to
- which signals indicate demand, risk, opportunity, or portfolio gaps
- where the authoritative product definitions live

ODPC provides the reusable portfolio objects for this work.

## What ODPC defines

The first version of ODPC focuses on these catalog objects:

- `Catalog`
- `ProductReference`
- `UseCase`
- `BusinessObjective`
- `Signal`

Together, these objects support discovery, portfolio planning, prioritization, governance review, AI-assisted analysis, and graph-based data product management.

## Quick example

Here is a minimal ODPC catalog:

```yaml
schema: https://opendataproducts.org/odpc-v1.0/schema/odpc.yaml
version: "1.0"

catalog:
  id: CAT-001
  name:
    en: Urban Mobility Data Product Catalog
  description:
    en: Catalog of data products, use cases, objectives, and signals related to urban mobility.
```

## Who should use ODPC?

Use ODPC when you need to manage data products as a portfolio, not just describe one product at a time. It is especially useful for data product catalogs, marketplaces, governance tools, portfolio reviews, AI agents, and graph-based operating models.

Learn more in the official [ODPC source repository](https://github.com/Open-Data-Product-Initiative/odpc-v1.0).

[BACK TO INDEX](https://github.com/Open-Data-Product-Initiative/odps-examples/blob/main/README.md)
