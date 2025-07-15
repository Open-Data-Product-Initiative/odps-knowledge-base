# What does a complete ODPS-compliant product look like?

A complete ODPS-compliant data product specification brings together all the necessary pieces to describe, manage, and govern a reusable data product.

Let’s break it down using the **UrbanPulse Events** product example.

---

## 1. Declare the Schema and Version

Every ODPS YAML starts by declaring the schema and version:

```yaml
schema: 'https://opendataproducts.org/v4.0/schema/odps.yaml'
version: 4.0
```

This line links the product to the ODPS v4.0 validation rules.

---

## 2. Add the Core Product Metadata

The `product.details` section includes human-readable information.

```yaml
product:
  details:
    en:
      name: UrbanPulse Events
      productID: urbanpulse-events-001
      valueProposition: Enable smarter city experiences ...
      description: UrbanPulse Events is a SmartCity data product ...
```

This tells users and machines what the product is, what it does, and how it fits into your domain.

---

## 3. Attach a Contract

The `product.contract` part connects to an external data usage agreement:

```yaml
contract:
  id: 02323M123
  type: ODCS
  contractVersion: 2.2.2
  contractURL: 'https://datamesh-manager.com/urbanltd/dataproducts/9bd530'
```

This keeps legal terms separate and versioned.

---

## 4. Define Pricing Plans

Each pricing tier is defined inside `pricingPlans.declarative`, referencing reusable specs.

```yaml
pricingPlans:
  declarative:
    en:
      - name: Basic Reader
        price: 0
        SLA:
          $ref: '#/Product/SLA/default'
        dataQuality:
          $ref: '#/Product/dataQuality/default'
```

Instead of repeating service levels, it uses references. This helps maintain consistency.

---

## 5. Configure Service Levels

SLAs, Data Quality, and Access methods are fully described and reusable.

```yaml
SLA:
  default:
    dimensions:
      - dimension: uptime
        objective: 90
        unit: percent
```

This can be used across pricing plans and even other products by copy or external reference.

---

## 6. Add Access and Payment Details

Define API or file-based access in the `dataAccess` block.

```yaml
dataAccess:
  API:
    outputPorttype: API
    accessURL: 'https://data.cms.gov/data-api/...'
```

Define payment logic with `paymentGateways`.

```yaml
paymentGateways:
  default:
    type: Stripe
    reference: 'https://docs.stripe.com/'
```

---

## 7. Add Support, License, and Data Holder Info

```yaml
support:
  email: support@opendataproducts.org

license:
  en:
    scope:
      rights:
        - Reproduction
        - Distribution

dataHolder:
  en:
    legalName: MindMote Oy
    email: contact@mindmote.fi
```

This makes the product self-contained and ready for publication or sale.

---

## ✅ Why This Structure Matters

- Validates automatically against the ODPS schema
- Supports AI-native discovery and integration
- Avoids duplication with reusable definitions
- Enforces quality and legal standards
- Works in APIs, data catalogs, and governance tools

---

➡️ **[View the full example YAML file here](yaml/full-example.yml)**

[BACK TO INDEX](https://github.com/Open-Data-Product-Initiative/odps-examples/blob/main/README.md)
