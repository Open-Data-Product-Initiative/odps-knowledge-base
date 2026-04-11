# 📄 How do I define product internal KPIs to measure product?

Within ODPS 4.1, `productKPIs` are part of the `productStrategy` object.
They describe the product-level metrics that show how the product is contributing to the business KPI defined in `contributesToKPI`.

---

## Where `productKPIs` belong

`productKPIs` is an optional array inside `product.productStrategy`.
The required `contributesToKPI` object defines the higher-level business KPI, while `productKPIs` define the measurable product metrics that support it.

### Example

```yaml
product:
  productStrategy:
    contributesToKPI:
      id: bizkpi-city-response-time
      name: City Emergency Response Time
      unit: minutes
      target: 5
      direction: at_most
      timeframe: "by Q4"
    productKPIs:
      - id: kpi-detection-coverage
        name: Event Detection Coverage
        description: % of reported incidents captured in real time
        unit: percentage
        target: 95
        direction: at_least
        frequency: hourly
        calculation: detected_events / reported_events
      - id: kpi-time-to-insight
        name: Average Time to Insight
        description: Median time from event occurrence to product update
        unit: seconds
        target: 60
        direction: at_most
        calculation: p50(update_ts - event_ts)
```

---

## Key fields for product KPIs

- `id`: Optional shared KPI identifier, useful for roll-ups and governance.
- `name`: The KPI label used in reports and dashboards.
- `description`: What the KPI measures and why it matters.
- `unit`: Measurement unit, such as `percentage`, `minutes`, or `seconds`.
- `target`: Desired value for the KPI.
- `direction`: One of `increase`, `decrease`, `at_least`, `at_most`, or `equals`.
- `frequency`: Optional measurement cadence (for example, `hourly`, `daily`, `monthly`).
- `calculation`: Optional formula describing how the KPI is computed.
- `owner`: Optional responsible role or team.

---

## How to choose product KPIs

1. Start with the primary business KPI in `contributesToKPI`.
2. Pick product measures that have a clear causal connection to that business outcome.
3. Include both leading and lagging indicators when possible.
4. Use `frequency` for metrics that need ongoing tracking.
5. Add `calculation` when the metric requires a definition beyond a simple count.

---

## Why product KPIs matter

`productKPIs` are useful when you want to:

- show how the data product impacts the business goal
- monitor operational performance of the product itself
- provide evidence for strategy reviews and governance checks
- support trade-off decisions between product improvements and business value

---

## Summary

Define `productKPIs` inside `productStrategy` to make product performance measurable and aligned with the business KPI your product supports.

[BACK TO INDEX](https://github.com/Open-Data-Product-Initiative/odps-examples/blob/main/README.md)
