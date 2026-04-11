![header image](resources/header.png)

# ODPS Knowledge Base

A practical reference for the Open Data Product Specification (ODPS). This repo combines learning resources, sample YAML, and FAQ guidance so teams can define data products in a consistent, interoperable way.

## Quick navigation

- [What is this repo?](#what-is-in-this-repo)
- [Browse the FAQ](#faq-with-examples)
- [Download the toolkit](#data-product-toolkit)
- [See the courses](#udemy-masterclasses)
- [Use the YAML builder](#yaml-builder-for-open-data-products)
- [External resources](#external-resources)
- [Raise an issue](https://github.com/Open-Data-Product-Initiative/odps-examples/issues)

## What is in this repo?

- `faq/` — curated question-and-answer pages with real ODPS examples
- `faq/yaml/` — companion YAML source examples for each FAQ topic
- `ODPS4/` — sample Open Data Product YAMLs for schema and product patterns
- `resources/` — toolkit files, visuals, and supporting downloads

## External resources

- [Accenture odps-python](https://github.com/Accenture/odps-python) — Python library for working with ODPS definitions programmatically

## Why use it?

- Learn ODPS through practical examples, not just specification text
- Copy and reuse proven YAML patterns for contracts, pricing, access, SLA, and DQ
- Find reusable components and reference patterns for production-ready metadata
- Access training, templates, and tools that speed up ODPS adoption

---

## FAQ with examples

This section helps you understand and apply the [ODPS specification](https://opendataproducts.org/) through practical, modular examples. Each answer includes:

- explanation of the concept
- plain YAML snippets
- full ODPS YAML examples in `faq/yaml`

### 📘 Core Concepts

- [What is ODPS, and why should I use it?](faq/what-is-odps.md)
- [What does a complete ODPS-compliant product look like?](faq/full-example.md)
- [What are the required and optional sections in ODPS?](faq/required-optional.md)
- [How do I define metadata for my data product?](faq/define-metadata.md)
- [How do I define related products and use cases?](faq/define-related.md)

### 📄 Contract & Licensing

- [How do I define a contract for my data product?](faq/contract.md)
- [How do I declare a license using ODPS?](faq/license.md)

### 💰 Pricing, Access & SLA

- [How do I define pricing plans?](faq/pricing.md)
- [Can I offer free and paid tiers in the same product?](faq/mixed-tiers.md)
- [How do I assign SLAs to pricing plans?](faq/sla-linking.md)
- [How do I define and reuse a payment gateway?](faq/payment-gateways.md)

### 🔁 Referencing & Reuse

- [How do I reuse SLA, DQ, and Access across products?](faq/reuse-components.md)
- [Can I reference external YAML files?](faq/external-ref.md)
- [What’s the difference between internal and external references?](faq/internal-vs-external-ref.md)

### ✅ Data Quality & Access Control

- [How do I define data quality rules?](faq/data-quality.md)
- [How do I specify access roles or visibility rules?](faq/access-control.md)

### 🤖 AI & Automation

- [How does ODPS support AI agent consumption?](faq/ai-agent-consumption.md)
- [How to use ODPS spec with LLMs.txt?](faq/odps-llms-txt.md)
- [How to build AI-assisted Minimum Lovable Governance with Claude?](https://github.com/Data-Maestro-Academy/DIY-MLG)

### 🛠️ Practical Use & Validation

- [How do I validate an ODPS spec in tools?](faq/validate.md)
- [How do I validate an ODPS YAML file?](faq/validation.md)
- [Are there templates I can use to start faster?](faq/templates.md)

> Each FAQ answer is stored in `/faq`, and most include a matching YAML example in `faq/yaml`.

---

## Data Product Toolkit

A free, open set of canvases for designing, measuring, and managing data products. Includes frameworks such as Data Product Canvas 2.1, Value Measure Framework, and Blueprint Model.

[Download the toolkit](./resources/Data_Product_Toolkit.pdf)

---

## Udemy MasterClasses

Apply ODPS in real-world business scenarios with structured training on monetization, governance, AI readiness, and product strategy.

- **[Master the Leading Data Product Specification with GPT tool](https://www.udemy.com/course/master-the-open-data-product-specification-with-gpt-tool/?referralCode=7602F38C9E58976291A3)**
  A focused introduction to ODPS for architects, business managers, and product owners.

- **[Data Product Monetization MasterClass](https://datamaestroacademy.com/courses/data-product-monetization)**
  Learn how to turn ODPS-based products into revenue-generating offerings, including pricing, AI monetization, and payment strategy.

- **[Data Product MasterClass](https://datamaestroacademy.com/courses/data-product-fundamentals)**
  Build a practical data product mindset with blueprints, examples, and execution guidance.

- **[Minimum Lovable Governance](https://datamaestroacademy.com/courses/data-product-governance)**
  Learn governance patterns that fit lean teams and support scalable data product delivery.

> These courses are designed to complement the documentation and examples in this repository.

---

## YAML Builder for Open Data Products

An AI-assisted tool for authoring and validating ODPS YAML. It helps generate schema-compliant output, but should be used with manual review.

- ODPS-compliant YAML generation
- Schema-aware guidance for contracts, access, pricing, SLA, and DQ
- Support for `$ref` and modular YAML structures
- Example-first output, ready for copy/paste

[Open ODPS GPT in OpenAI](https://chatgpt.com/g/g-687a26b92c20819182e92a8641fbd02f-yaml-builder-for-open-data-products)

---

## Need help?

If you cannot find what you are looking for, please [raise an issue](https://github.com/Open-Data-Product-Initiative/odps-examples/issues) and describe your need.
