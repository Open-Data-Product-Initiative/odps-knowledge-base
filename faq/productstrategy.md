# 📄 How do I define a product strategy and what is it?

ODPS 4.1 introduces the `productStrategy` object inside `product` to link a data product directly to business outcomes.
This object makes the product’s purpose explicit, shows which business KPI it contributes to, and describes how success is measured.

---

## What does `productStrategy` do?

`productStrategy` connects your product to business objectives and measurable outcomes.
It is designed to help teams:

- align the product with strategic goals
- declare the primary business KPI the product is accountable for
- define optional product-level KPIs that show how the product contributes
- track related KPIs for secondary impacts or cross-unit value
- capture status, planning dates, and strategic alignment statements

---

## Structure of `productStrategy`

The object is defined under `product:` and can contain these main fields:

- `objectives`: one or more business objectives in natural language
- `strategicAlignment`: references to corporate initiatives, visions, or policies
- `contributesToKPI`: the required primary business KPI the product supports
- `relatedKPIs`: optional secondary KPIs for side effects or broader impact
- `productKPIs`: optional product-level KPIs that feed the main KPI
- `status`, `startDate`, `endDate`, `description`

### Example

```yaml
product:
  productStrategy:
    status: Active
    startDate: 2026-01-01
    endDate: 2026-12-31
    objectives:
      - en: Reduce emergency response time for city services
    strategicAlignment:
      - en: Smart City Vision 2030
    contributesToKPI:
      id: bizkpi-city-response-time
      name: City Emergency Response Time
      description: Average minutes from incident to first responder arrival
      unit: minutes
      target: 5
      direction: at_most
      timeframe: "by Q4"
    relatedKPIs:
      - id: bizkpi-traffic-congestion
        name: Traffic Congestion Index
        unit: percentage
        target: -10
        direction: decrease
    productKPIs:
      - id: kpi-detection-coverage
        name: Event Detection Coverage
        unit: percentage
        target: 95
        direction: at_least
        frequency: hourly
        calculation: detected_events / reported_events
```

---

## Key fields explained

- `contributesToKPI`: Required. Identifies the higher-level business KPI the product is primarily accountable for.
- `objectives`: Business outcome statements that explain why the product exists.
- `strategicAlignment`: References business initiatives, programs, or strategic visions.
- `productKPIs`: Product-specific metrics that contribute to the main KPI.
- `relatedKPIs`: Secondary or cross-unit measures that help track side effects or additional value.
- `status`, `startDate`, `endDate`: Lifecycle and planning metadata for the strategy.

---

## Why use it?

Use `productStrategy` when you want to make the business case of a data product explicit and machine-readable. It improves:

- strategic transparency
- governance and prioritization
- product-to-business alignment
- measurement and accountability

---

## Summary

`productStrategy` is the ODPS object for business intent and KPI linkage. It helps teams write the product’s "why" alongside the product’s "what" and "how".

[BACK TO INDEX](https://github.com/Open-Data-Product-Initiative/odps-examples/blob/main/README.md)
