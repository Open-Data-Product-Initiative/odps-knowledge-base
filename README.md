<p align="center">
  <img src="resources/header.png" alt="ODPS Knowledge Base" width="100%">
</p>

<h1 align="center">ODPS Knowledge Base</h1>

<p align="center">
  A practical reference for the <strong>Open Data Product Specification (ODPS)</strong>, combining learning resources, sample YAML, reusable patterns, and FAQ guidance for interoperable data products.
</p>

<p align="center">
  <a href="https://opendataproducts.org/"><img alt="ODPS specification" src="https://img.shields.io/badge/ODPS-Specification-0B5FFF"></a>
  <a href="#faq-with-examples"><img alt="FAQ examples" src="https://img.shields.io/badge/FAQ-Examples-198754"></a>
  <a href="#data-product-toolkit-and-python-library"><img alt="Resources" src="https://img.shields.io/badge/Resources-Toolkit%20%26%20Library-6F42C1"></a>
  <a href="https://github.com/Open-Data-Product-Initiative/odps-examples/issues"><img alt="Raise an issue" src="https://img.shields.io/badge/Support-Raise%20an%20Issue-FD7E14"></a>
</p>

<br>

<table>
  <tr>
    <td><strong>Browse the FAQ</strong></td>
    <td>Learn ODPS and ODPC concepts through practical answers and implementation examples.</td>
    <td><a href="#faq-with-examples">Open FAQ</a></td>
  </tr>
  <tr>
    <td><strong>Use example YAML</strong></td>
    <td>Copy reusable patterns for contracts, pricing, access, SLA, data quality, and references.</td>
    <td><a href="faq/yaml">View YAML</a></td>
  </tr>
  <tr>
    <td><strong>Download resources</strong></td>
    <td>Access the Data Product Toolkit, governance whitepaper, and ODPS Python library.</td>
    <td><a href="#data-product-toolkit-and-python-library">Get resources</a></td>
  </tr>
  <tr>
    <td><strong>Build with AI assistance</strong></td>
    <td>Use the YAML Builder GPT to author and validate ODPS 4.0 YAML faster.</td>
    <td><a href="#yaml-builder-for-open-data-products">Open builder</a></td>
  </tr>
</table>

## What is in this repo?

<table>
  <tr>
    <th>Directory</th>
    <th>Purpose</th>
  </tr>
  <tr>
    <td><code>faq/</code></td>
    <td>Curated question-and-answer pages with real ODPS examples.</td>
  </tr>
  <tr>
    <td><code>faq/yaml/</code></td>
    <td>Companion YAML source examples for each FAQ topic.</td>
  </tr>
  <tr>
    <td><code>ODPS4/</code></td>
    <td>Sample Open Data Product YAMLs for schema and product patterns.</td>
  </tr>
  <tr>
    <td><code>resources/</code></td>
    <td>Toolkit files, visuals, and supporting downloads.</td>
  </tr>
</table>

## Why use it?

<table>
  <tr>
    <td><strong>Example-first learning</strong></td>
    <td>Understand ODPS through applied examples rather than specification text alone.</td>
  </tr>
  <tr>
    <td><strong>Reusable YAML patterns</strong></td>
    <td>Adapt proven structures for contracts, pricing, access, SLA, and data quality.</td>
  </tr>
  <tr>
    <td><strong>Production-ready references</strong></td>
    <td>Find reusable components and metadata patterns for real data product work.</td>
  </tr>
  <tr>
    <td><strong>Adoption support</strong></td>
    <td>Use training, templates, and tools that help teams move faster with ODPS.</td>
  </tr>
</table>

---

## FAQ with examples

This section helps you understand and apply the [ODPS specification](https://opendataproducts.org/) and related OpenDataProducts.org standards through practical, modular examples. Each answer includes:

- explanation of the concept
- plain YAML snippets
- full ODPS YAML examples in `faq/yaml`

### 📘 Core Concepts

- [What is ODPS, and why should I use it?](faq/what-is-odps.md)
- [What does a complete ODPS-compliant product look like?](faq/full-example.md)
- [What are the required and optional sections in ODPS?](faq/required-optional.md)
- [How do I define metadata for my data product?](faq/define-metadata.md)
- [How do I define related products and use cases?](faq/define-related.md)

### 🗂️ ODPC Catalogs and Portfolio Management

- [What is ODPC, and why should I use it?](faq/what-is-odpc.md)
- [What is the difference between ODPC, ODPS, and ODPG?](faq/odpc-vs-odps.md)
- [What does a simple ODPC catalog look like?](faq/odpc-catalog-example.md)
- [How do I use ProductReference in ODPC?](faq/odpc-product-reference.md)

### 📄 Product Strategy and linking to Business Objectives

- [How do I define a product strategy and what is it?](faq/productstrategy.md)
- [How do I define product internal KPIs to measure product?](faq/productKPIs.md)

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

## Data Product Toolkit and Python Library

<table>
  <tr>
    <th>Resource</th>
    <th>Description</th>
    <th>Link</th>
  </tr>
  <tr>
    <td><strong>Data Product Toolkit</strong></td>
    <td>A free, open set of canvases for designing, measuring, and managing data products, including Data Product Canvas 2.1, Value Measure Framework, and Blueprint Model.</td>
    <td><a href="./resources/Data_Product_Toolkit.pdf">Download</a></td>
  </tr>
  <tr>
    <td><strong>Minimum Lovable Governance Whitepaper</strong></td>
    <td>Guidance for data product governance, operating models, and lightweight adoption patterns.</td>
    <td><a href="https://github.com/Open-Data-Product-Initiative/odps-knowledge-base/blob/main/resources/Minimum%20Lovable%20Governance%20for%20Data%20Products%20Whitepaper.pdf">Read</a></td>
  </tr>
  <tr>
    <td><strong>ODPS Python Library</strong></td>
    <td>A comprehensive, high-performance Python library for creating, validating, and manipulating ODPS v4.0 documents with international standards compliance.</td>
    <td><a href="https://github.com/Accenture/odps-python">Get library</a></td>
  </tr>
</table>

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

An AI-assisted tool for authoring and validating ODPS 4.0 YAML. It helps generate schema-compliant output, but should be used with manual review.

- ODPS-compliant YAML generation
- Schema-aware guidance for contracts, access, pricing, SLA, and DQ
- Support for `$ref` and modular YAML structures
- Example-first output, ready for copy/paste

[Open ODPS GPT in OpenAI](https://chatgpt.com/g/g-687a26b92c20819182e92a8641fbd02f-yaml-builder-for-open-data-products)

---

## Need help?

If you cannot find what you are looking for, please [raise an issue](https://github.com/Open-Data-Product-Initiative/odps-examples/issues) and describe your need.
