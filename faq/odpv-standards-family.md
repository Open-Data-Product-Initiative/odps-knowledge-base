# How does ODPV relate to ODPS, ODPC, and ODPG?

ODPV is the shared vocabulary layer for the OpenDataProducts.org standards family. It does not replace ODPS, ODPC, or ODPG. It gives them stable terms, labels, definitions, and relationship names they can reference.

## Short answer

- **ODPS defines one data product.**
- **ODPC defines reusable catalog and portfolio objects.**
- **ODPG defines relationships between products, use cases, objectives, KPIs, signals, and other objects.**
- **ODPV defines the shared language used by all of them.**

## What ODPV adds

ODPV prevents duplicate or conflicting definitions for common terms such as:

- `DataProduct`
- `UseCase`
- `BusinessObjective`
- `KPI`
- `Signal`
- `Owner`
- `SLA`
- `License`
- `AccessMethod`
- `supports`
- `contributesTo`
- `governedBy`

Instead of every specification redefining those terms locally, ODPV provides one vocabulary reference point.

## Practical examples

An ODPS data product can reference ODPV terms such as `DataProduct`, `Owner`, `SLA`, `DataQuality`, `License`, and `AccessMethod`.

An ODPC catalog can reference ODPV terms such as `DataProductCatalog`, `UseCase`, `BusinessObjective`, `KPI`, `Signal`, `Gap`, and `Priority`.

An ODPG graph can use ODPV relationship terms such as `supports`, `requires`, `contributesTo`, `measures`, `belongsTo`, `dependsOn`, `governedBy`, `providedBy`, `consumedBy`, and `indicates`.

## Rule of thumb

Use **ODPV** when the question is "Which shared term or relationship name should we use?"

Use **ODPS** when the question is "How do we define this data product?"

Use **ODPC** when the question is "How do we catalog this portfolio?"

Use **ODPG** when the question is "How are these objects connected?"

[BACK TO INDEX](https://github.com/Open-Data-Product-Initiative/odps-examples/blob/main/README.md)
