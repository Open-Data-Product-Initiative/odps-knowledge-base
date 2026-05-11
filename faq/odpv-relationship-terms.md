# How do I use ODPV relationship terms?

ODPV relationship terms provide controlled names for connecting data products, catalogs, use cases, objectives, KPIs, signals, providers, consumers, policies, and other portfolio objects.

ODPV defines the relationship names and meanings. ODPG defines how those relationship types are used in graph structures.

## Common relationship terms

Use these ODPV relationship terms when building portfolio graphs or graph-ready catalog metadata:

- `supports`: one object helps enable another object, such as a data product supporting a use case
- `requires`: one object needs another object to be useful or executable
- `contributesTo`: one object helps advance another object, such as a use case contributing to a business objective
- `measures`: one object measures another object, such as a KPI measuring an objective
- `belongsTo`: one object is grouped under another object, such as a data product belonging to a catalog
- `dependsOn`: one object has a dependency on another object
- `governedBy`: one object is governed by a license, policy, agreement, or compliance rule
- `providedBy`: one object is provided, published, or made available by a provider
- `consumedBy`: one object is used, accessed, or consumed by a consumer
- `indicates`: one object points to another object, such as a signal indicating a gap or opportunity

## Example term definition

```yaml
id: supports
uri: https://opendataproducts.org/odpv-v1.0/terms/supports
type: relationship
status: stable
introducedIn: 1.0.0
preferredLabel:
  en: supports
definition:
  en: Indicates that one object helps enable, serve, or make another object possible, such as a data product supporting a use case.
alsoKnownAs:
  en:
    - enables
    - serves
    - helps
    - provides support for
relatedTerms:
  - contributesTo
  - requires
  - relatedTo
usedIn:
  - ODPG
```

## Practical use

In a graph implementation, ODPV terms help keep edge names consistent:

```yaml
relationships:
  - from: DP-001
    type: supports
    to: UC-001
  - from: UC-001
    type: contributesTo
    to: BO-001
  - from: KPI-001
    type: measures
    to: BO-001
```

## Summary

Use ODPV relationship terms as the shared vocabulary for graph edges. Use ODPG when you need the full graph structure and rules.

[BACK TO INDEX](https://github.com/Open-Data-Product-Initiative/odps-examples/blob/main/README.md)
