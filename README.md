<p align="center">
  <img src="resources/open-data-product-standards-hero.png" alt="Open Data Product Standards Knowledge Base" width="100%">
</p>

<h1 align="center">Open Data Product Standards Knowledge Base</h1>

<p align="center">
  A practical knowledge space for the <strong>OpenDataProducts.org standards family</strong>, including ODPS, ODPC, ODPV, and future ODPG guidance.
</p>

<p align="center">
  <a href="#odps-open-data-product-specification"><img alt="ODPS specification" src="https://img.shields.io/badge/ODPS-Specification-7C3AED"></a>
  <a href="#odpc-catalogs-and-portfolio-management"><img alt="ODPC catalogs" src="https://img.shields.io/badge/ODPC-Catalogs-F97316"></a>
  <a href="#odpv-vocabulary-and-shared-terms"><img alt="ODPV vocabulary" src="https://img.shields.io/badge/ODPV-Vocabulary-0EA5E9"></a>
  <a href="#odpg-open-data-product-graphs-coming-soon"><img alt="ODPG graphs" src="https://img.shields.io/badge/ODPG-Graphs-22C55E"></a>
  <a href="#faq-with-examples"><img alt="FAQ examples" src="https://img.shields.io/badge/FAQ-Examples-198754"></a>
  <a href="#data-product-toolkit-and-python-library"><img alt="Resources" src="https://img.shields.io/badge/Resources-Toolkit%20%26%20Library-64748B"></a>
  <a href="https://github.com/Open-Data-Product-Initiative/odps-examples/issues"><img alt="Raise an issue" src="https://img.shields.io/badge/Support-Raise%20an%20Issue-64748B"></a>
</p>

<p align="center">
  <a href="#faq-with-examples"><strong>Browse FAQ</strong></a>
  ·
  <a href="faq/yaml"><strong>View YAML examples</strong></a>
  ·
  <a href="#specification-tools"><strong>Use specification tools</strong></a>
  ·
  <a href="#data-product-toolkit-and-python-library"><strong>Get resources</strong></a>
  ·
  <a href="#udemy-masterclasses"><strong>See training</strong></a>
</p>

## What is in this repo?

- `faq/`: practical Q&A pages for ODPS, ODPC, ODPV, and future ODPG guidance.
- `faq/yaml/`: companion YAML examples for product specs, catalogs, vocabulary terms, contracts, pricing, access, SLA, data quality, and references.
- `ODPS4/`: sample Open Data Product YAMLs for schema and product patterns.
- `resources/`: toolkit files, visuals, whitepapers, and supporting downloads.
- [Udemy MasterClasses](#udemy-masterclasses): structured training for ODPS, data product monetization, data product mindset, and minimum lovable governance.

## Why use it?

- Learn through applied examples rather than specification text alone.
- Reuse proven YAML patterns across product specs, catalogs, vocabulary, and governance.
- Find production-ready references for real data product work.
- Combine FAQs, templates, Python tools, training, and AI assistance in one place.

---

## FAQ with examples

This section helps you understand and apply the OpenDataProducts.org standards family through practical, modular examples. The FAQs are grouped by specification so you can start with the standard you are using.

- explanation of the concept
- plain YAML snippets
- companion YAML examples in `faq/yaml`

<a id="odps-open-data-product-specification"></a>

### 🟣 ODPS: Open Data Product Specification

<p>
  <img alt="ODPS color marker" src="https://img.shields.io/badge/ODPS-Specification-7C3AED">
</p>

Use these when you are defining one data product and its metadata, contract, pricing, access, quality, and validation rules.

**Core concepts**

- [What is ODPS, and why should I use it?](faq/what-is-odps.md)
- [What does a complete ODPS-compliant product look like?](faq/full-example.md)
- [What are the required and optional sections in ODPS?](faq/required-optional.md)
- [How do I define metadata for my data product?](faq/define-metadata.md)
- [How do I define related products and use cases?](faq/define-related.md)

**Strategy and business value**

- [How do I define a product strategy and what is it?](faq/productstrategy.md)
- [How do I define product internal KPIs to measure product?](faq/productKPIs.md)

**Contract and licensing**

- [How do I define a contract for my data product?](faq/contract.md)
- [How do I declare a license using ODPS?](faq/license.md)

**Pricing, access, and service levels**

- [How do I define pricing plans?](faq/pricing.md)
- [Can I offer free and paid tiers in the same product?](faq/mixed-tiers.md)
- [How do I assign SLAs to pricing plans?](faq/sla-linking.md)
- [How do I define and reuse a payment gateway?](faq/payment-gateways.md)

**Reuse, quality, and validation**

- [How do I reuse SLA, DQ, and Access across products?](faq/reuse-components.md)
- [Can I reference external YAML files?](faq/external-ref.md)
- [What’s the difference between internal and external references?](faq/internal-vs-external-ref.md)
- [How do I define data quality rules?](faq/data-quality.md)
- [How do I specify access roles or visibility rules?](faq/access-control.md)
- [How do I validate an ODPS spec in tools?](faq/validate.md)
- [How do I validate an ODPS YAML file?](faq/validation.md)
- [Are there templates I can use to start faster?](faq/templates.md)

<a id="odpc-catalogs-and-portfolio-management"></a>

### 🟠 ODPC Catalogs and Portfolio Management

<p>
  <img alt="ODPC color marker" src="https://img.shields.io/badge/ODPC-Catalogs-F97316">
</p>

Use these when you are cataloging a portfolio of data products, use cases, business objectives, signals, and product references.

- [What is ODPC, and why should I use it?](faq/what-is-odpc.md)
- [What is the difference between ODPC, ODPS, and ODPG?](faq/odpc-vs-odps.md)
- [What does a simple ODPC catalog look like?](faq/odpc-catalog-example.md)
- [How do I use ProductReference in ODPC?](faq/odpc-product-reference.md)
- [What Python tools are available for ODPC?](faq/odpc-python-tools.md)

<a id="odpv-vocabulary-and-shared-terms"></a>

### 🔵 ODPV Vocabulary and Shared Terms

<p>
  <img alt="ODPV color marker" src="https://img.shields.io/badge/ODPV-Vocabulary-0EA5E9">
</p>

Use these when you need controlled vocabulary terms for data product objects, value concepts, governance concepts, and graph relationship names.

- [What is ODPV, and why should I use it?](faq/what-is-odpv.md)
- [How does ODPV relate to ODPS, ODPC, and ODPG?](faq/odpv-standards-family.md)
- [What are the main ODPV vocabulary groups?](faq/odpv-vocabulary-groups.md)
- [How do I use ODPV relationship terms?](faq/odpv-relationship-terms.md)
- [What Python tools are available for ODPV?](faq/odpv-python-tools.md)

<a id="odpg-open-data-product-graphs-coming-soon"></a>

### 🟢 ODPG: Open Data Product Graphs Coming Soon

<p>
  <img alt="ODPG color marker" src="https://img.shields.io/badge/ODPG-Graphs-22C55E">
</p>

Use this section for future graph FAQs about connecting data products, catalogs, use cases, objectives, KPIs, signals, governance objects, providers, and consumers.

### 🤖 Cross-standard AI and Automation

- [How does ODPS support AI agent consumption?](faq/ai-agent-consumption.md)
- [How to use ODPS spec with LLMs.txt?](faq/odps-llms-txt.md)
- [How to build AI-assisted Minimum Lovable Governance with Claude?](https://github.com/Data-Maestro-Academy/DIY-MLG)

> Each FAQ answer is stored in `/faq`, and most include a matching YAML example in `faq/yaml`.

---

## Specification Tools

Some OpenDataProducts.org specifications include Python utilities for validation, artifact generation, search, and AI-agent-friendly workflows.

<table>
  <tr>
    <th>Standard</th>
    <th>Tools</th>
    <th>Use for</th>
    <th>Source</th>
  </tr>
  <tr>
    <td><strong>ODPC</strong></td>
    <td><code>validate_catalog.py</code>, <code>explain_catalog.py</code>, <code>search_objects.py</code>, <code>generate_catalog_artifacts.py</code>, <code>check_agent_artifacts.py</code></td>
    <td>Validate catalog files, summarize catalogs, search catalog object guidance, and keep generated catalog artifacts in sync.</td>
    <td><a href="https://github.com/Open-Data-Product-Initiative/odpc-v1.0/tree/main/scripts">ODPC scripts</a></td>
  </tr>
  <tr>
    <td><strong>ODPV</strong></td>
    <td><code>validate_vocab.py</code>, <code>generate_vocab_artifacts.py</code>, <code>search_vocab.py</code>, <code>vocab_utils.py</code></td>
    <td>Validate vocabulary files, regenerate derived vocabulary artifacts, and search controlled vocabulary terms.</td>
    <td><a href="https://github.com/Open-Data-Product-Initiative/odpv-v1.0/tree/main/scripts">ODPV scripts</a></td>
  </tr>
</table>

See the FAQ entries for [ODPC Python tools](faq/odpc-python-tools.md) and [ODPV Python tools](faq/odpv-python-tools.md) for command examples.

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

- **[Data Product Monetization MasterClass](https://www.udemy.com/course/data-product-monetization-masterclass/?referralCode=53941B985FBFA582CBC7)**
  Learn how to turn ODPS-based products into revenue-generating offerings, including pricing, AI monetization, and payment strategy.

- **[Data Product MasterClass](https://www.udemy.com/course/data-product-mindset/?referralCode=548AA9F02E100D61D284)**
  Build a practical data product mindset with blueprints, examples, and execution guidance.

- **[Minimum Lovable Governance](https://www.udemy.com/course/data-products-minimum-lovable-governance-masterclass/?referralCode=3A5188B67577CFBC0B18)**
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
