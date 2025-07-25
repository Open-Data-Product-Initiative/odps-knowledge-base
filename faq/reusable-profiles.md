# 🧩 ODPS 4.0 Reusable Profile Templates

Welcome to the official repository of **reusable profile templates** for the [Open Data Product Specification (ODPS) 4.0](https://opendataproducts.org/v4.0).

This library helps you accelerate adoption, enforce consistency, and scale governance across all your data products by referencing shared metadata blocks using `$ref`.

---

## 🔍 What Are Profile Templates?

ODPS 4.0 introduces **in-spec referencing** — a powerful feature that allows your data products to reuse predefined YAML profiles for:

- ✅ SLAs
- ✅ Data quality tiers
- ✅ Access configurations
- ✅ Pricing plans
- ✅ Licenses
- ✅ Payment gateways

Instead of duplicating metadata in every product spec, you define a profile once and reference it using `$ref`.

---

## ✨ Benefits of Using Shared Profiles

- **Consistency by design**  
- **Faster onboarding of new data products**  
- **Centralized governance with cascading updates**  
- **Alignment with Medallion Architecture tiers (Bronze, Silver, Gold)**  
- **Cleaner YAML, fewer copy-paste errors**  
- **Improved interoperability and AI-readiness**

---

## Referencing Example

From inside your ODPS product YAML:

```yaml
SLA:
    declarative:
        gold:
            $ref: 'https://opendataproducts.org/profiles/SLA/gold.yaml'
```

## Available Profiles

| Type             | Profile Name       | Path/Link                                                      |
| ---------------- | ------------------ | -------------------------------------------------------------- |
| **Coming**          | `gold`             | [`SLA/gold.yaml`](./SLA/gold.yaml)                          |



## Contributing

Want to propose a new reusable profile?

* Fork this repo
* Add your YAML profile under the correct folder (/SLA/, /dataAccess/, etc.)
* Submit a pull request with a short description in the PR body

We'll review and merge useful, valid profiles into the public template library.

## Best Practices

* Use semantic naming (gold, silver, partner, freemium)
* Add comments to clarify use cases
* Version profiles if needed (e.g., gold.v1.yaml)
* Keep references relative when using locally
* Use URLs when publishing centrally (e.g., via CDN or documentation site)

