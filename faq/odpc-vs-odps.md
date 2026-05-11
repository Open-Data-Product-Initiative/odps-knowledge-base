# What is the difference between ODPC, ODPS, and ODPG?

ODPC, ODPS, and ODPG are complementary specifications in the OpenDataProducts.org standards family. Each one has a separate responsibility.

## Short answer

- **ODPS defines the product.**
- **ODPC defines reusable portfolio objects.**
- **ODPG defines the relationships between those objects.**

This separation keeps each specification focused and easier to adopt.

## ODPS: one data product

ODPS, the Open Data Product Specification, describes a single data product in detail. It can define product metadata, data access, contracts, pricing, licensing, service levels, data quality, support, and other product-specific information.

Use ODPS when you need an authoritative definition of one data product.

## ODPC: the catalog and portfolio layer

ODPC, the Open Data Product Catalogs specification, describes reusable catalog objects around data products. It does not replace the full product definition.

Use ODPC to describe:

- catalogs
- product references
- use cases
- business objectives
- signals
- ownership, scope, status, tags, and portfolio metadata

ODPC can point to ODPS files, but it can also reference other product models such as internal templates, marketplace definitions, vendor catalog assets, or other machine-readable descriptors.

## ODPG: relationships and graph structure

ODPG, Open Data Product Graphs, defines relationships between catalog objects. For example, it can express that a product supports a use case, a use case contributes to a business objective, or a signal reveals a portfolio gap.

ODPC defines the objects. ODPG connects them.

## Practical rule of thumb

Use **ODPS** when the question is "What is this data product and how can it be consumed?"

Use **ODPC** when the question is "What products, use cases, objectives, and signals exist in this portfolio?"

Use **ODPG** when the question is "How are these products, use cases, objectives, and signals connected?"

[BACK TO INDEX](https://github.com/Open-Data-Product-Initiative/odps-examples/blob/main/README.md)
