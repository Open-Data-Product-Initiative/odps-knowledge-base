# What does a simple ODPC catalog look like?

A simple ODPC catalog defines a portfolio container and can include product references, use cases, business objectives, and signals.

The catalog should organize portfolio-level information. It should not duplicate the full details of each data product. Detailed product metadata belongs in the authoritative product model, such as ODPS.

## Minimal catalog

Every ODPC catalog starts with the schema, version, and `catalog` object:

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

## Add portfolio context

You can add ownership, scope, lifecycle status, graph information, and tags:

```yaml
catalog:
  id: CAT-001
  name:
    en: Urban Mobility Data Product Catalog
  description:
    en: Catalog of data products, use cases, objectives, and signals related to urban mobility.
  owner:
    organization: Example Transport Authority
    team: Business Analytics
    role: Data Product Portfolio Manager
  scope:
    domains:
      - smart-city
      - mobility
      - transport
    geography: Abu Dhabi
    audience:
      - internal
      - public
  status: active
  graph:
    standard: ODPG
    version: "1.0"
    uri: https://example.org/graphs/urban-mobility.graph.yaml
```

## Add reusable catalog objects

An ODPC catalog can include product references, use cases, business objectives, and signals:

```yaml
productReferences:
  - id: DP-001
    productID: urbanpulse-events
    productVersion: "1.0.0"
    name:
      en: UrbanPulse Events Data Product
    description:
      en: Event information for urban analytics and citizen services.
    productModel:
      standard: ODPS
      version: "4.1"
      format: yaml
      uri: https://example.org/products/urbanpulse-events/odps.yaml

useCases:
  - id: UC-001
    name:
      en: Event Demand Forecasting
    description:
      en: Forecast event-related demand to improve mobility planning and citizen services.

businessObjectives:
  - id: BO-001
    name:
      en: Improve Urban Mobility Efficiency
    description:
      en: Reduce travel delays and improve city movement through better data-driven planning.

signals:
  - id: SIG-001
    name:
      en: Increasing Event Demand
    description:
      en: Demand for event-related mobility and public service planning is increasing.
    type: demand
    source:
      origin: internal
      method: usage_analysis
    observedAt: 2026-04-18T09:30:00Z
```

➡️ **[View the full ODPC catalog YAML example here](yaml/odpc-catalog.yml)**

[BACK TO INDEX](https://github.com/Open-Data-Product-Initiative/odps-examples/blob/main/README.md)
