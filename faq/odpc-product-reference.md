# How do I use ProductReference in ODPC?

`ProductReference` is the ODPC object for adding a data product to a catalog without copying the full product definition into the catalog.

It should include enough information for discovery, filtering, portfolio review, and display. The detailed product definition should stay in the authoritative product model, such as an ODPS YAML file.

## What belongs in ProductReference?

A product reference should identify:

- the product reference ID
- the product ID and version
- the product name and short description
- the product model standard, version, format, and URI

## Minimal example

```yaml
productReference:
  id: DP-001
  productID: urbanpulse-events
  productVersion: "1.0.0"
  name:
    en: UrbanPulse Events Data Product
  description:
    en: Data product providing event information for urban analytics and citizen services.
  productModel:
    standard: ODPS
    version: "4.1"
    format: yaml
    uri: https://example.org/products/urbanpulse-events/odps.yaml
```

## What should not be duplicated?

Keep `ProductReference` lightweight. Do not copy detailed product metadata into the catalog when it already belongs in ODPS or another source model.

Avoid duplicating:

- data access methods
- SLA definitions
- data quality rules
- pricing plans
- license terms
- support details
- technical interface details

## Optional discovery fields

You can add lightweight fields that help catalog users search, filter, and prioritize products:

```yaml
productReference:
  id: DP-001
  productID: urbanpulse-events
  productVersion: "1.0.0"
  name:
    en: UrbanPulse Events Data Product
  description:
    en: Event information for urban analytics and citizen services.
  valueProposition:
    en: Supports event-based mobility planning and citizen services.
  visibility: public
  status: production
  type: dataset
  domains:
    - smart-city
    - mobility
  tags:
    - events
    - smart-city
    - mobility
  portfolioPriority: high
  owner:
    organization: Example Organization
    team: Urban Analytics
    role: Data Product Owner
  productModel:
    standard: ODPS
    version: "4.1"
    format: yaml
    uri: https://example.org/products/urbanpulse-events/odps.yaml
```

## Summary

Use `ProductReference` as the catalog card for a product. Use ODPS, or another product model, as the detailed product definition.

[BACK TO INDEX](https://github.com/Open-Data-Product-Initiative/odps-examples/blob/main/README.md)
