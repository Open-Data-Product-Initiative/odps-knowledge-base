# Guide 19: Work with OpenMetadata

Use the Open Data Products SDK to discover OpenMetadata data products, export an
ODPC catalog or an ODPS product, and review changes before writing to the
platform. You can also manage domains and attach an ODCS contract.

**Availability:** This guide describes the experimental integration in the
[SDK GitHub commit](https://github.com/Open-Data-Product-Initiative/odp-agent-sdk/commit/7036a9730107b357a047a78371ce6301bda89e6e)
that prepares version 0.8.0. As of 25 November 2026, this commit is on the
`feat/odpv-profile-interop` branch, while the default branch and PyPI release
0.7.0 do not include the integration. Install the pinned commit below; the
interface may change. Examples use a POSIX shell.

The SDK integration has been tested against one OpenMetadata 2.1.0 deployment;
behavior and permissions may differ elsewhere. Product creation and permanent
deletion are restricted to 2.1.0. A connection check establishes read access
only, not write permission. Imported metadata is a source's statement, not
proof of business approval or data quality.

## 1. Install the integration-capable SDK

In a virtual environment with Git installed, install the tested SDK commit from
GitHub:

```sh
python -m pip install "open-data-products @ git+https://github.com/Open-Data-Product-Initiative/odp-agent-sdk.git@7036a9730107b357a047a78371ce6301bda89e6e"
open-data-products openmetadata products --help
open-data-products integrations --help
```

If these commands are missing, check which SDK installation is active. This
integration does not require the OpenMetadata Python SDK. See [Guide 0](../00-setup-python/)
for virtual environment setup.

## 2. Configure a connection

Copy the [example configuration](connections.example.yaml) to a private working
location, edit `base_url`, and obtain a bearer token from your OpenMetadata
administrator. Both a root URL and one ending in `/api` are supported; retain
any deployment path prefix. The example starts read-only.

```sh
cp sdk/19-openmetadata-integration/connections.example.yaml ~/connections.yaml
# Set OPENMETADATA_TOKEN in your shell or secret manager without committing it.
open-data-products integrations list --config ~/connections.yaml
open-data-products connect openmetadata --config ~/connections.yaml
```

Run the copy command from the knowledge-base repository root. Set the token as
an environment variable before connecting; the SDK does not automatically load
`.env` files. Keep tokens, private URLs and retrieved customer metadata out of
version control. TLS verification is enabled by default; configure `ca_bundle`
for a private CA. Plain HTTP needs `allow_insecure_http: true` and sends the
bearer token unencrypted.

`connect` checks connectivity and saves the configuration path and profile name
in `.open-data-products/integrations.yaml` in the current working directory,
without storing the token. Run the remaining short commands from that directory.
Use `--config ~/connections.yaml` and optionally `--connection openmetadata` to
override the saved selection. A different config without a connection uses its
default profile.

## 3. Discover products and domains

```sh
open-data-products integrations domains openmetadata --config ~/connections.yaml --json
open-data-products openmetadata products list --json
open-data-products openmetadata products search "customer" --limit 20 --json
open-data-products openmetadata products get PRODUCT_UUID --json
open-data-products openmetadata products get PRODUCT_UUID --format odps --json
```

Replace `PRODUCT_UUID` with an actual platform UUID. The short `get` command
also accepts an exact name or display name; ambiguous matches require an
interactive selection, so use UUIDs in scripts. Its default format is native;
`--format odps` requests the platform's ODPS export.

List and search return validated ODPC 1.0 catalogs, with references to native
OpenMetadata product records. Full listing follows pages and rejects incomplete
pagination; search returns one page and supports `--offset` and `--limit`.
Search uses the platform index and may lag behind changes. Results are limited
by the token's platform permissions, and neither operation is an atomic
snapshot. The OpenMetadata metadata revision is mapped to `productVersion` and
labelled as such; it is not an independently verified product release version.
Unlabelled source text is mapped to the required English field without
translation. Catalog validation does not validate the underlying data or
contracts.

Export the listing to a new file and validate it locally:

```sh
open-data-products openmetadata products export --output catalog.yaml
open-data-products validate catalog.yaml --json
```

Existing output files are not overwritten.

## 4. Retrieve and compare an ODPS product

The explicit integration command can save the ODPS export and provenance:

```sh
open-data-products integrations products get openmetadata \
  --config ~/connections.yaml --id PRODUCT_UUID \
  --output product.yaml --provenance product.provenance.json
open-data-products validate product.yaml
open-data-products openmetadata products compare --id PRODUCT_UUID \
  --source product.yaml --domain YOUR_DOMAIN --json
```

The export retains its source ODPS version and is validated locally. Strict
validation is on by default: invalid exports are not saved. To inspect an
invalid export, add `--strict false`; the SDK saves it with a separate
`.validation.json` findings file and exits successfully with a warning. For
numeric `updated` timestamps, `--normalize-updated-timestamps` requires both
`--output` and `--provenance`; it keeps the original, records the conversion
and validates the derived document. Other validation errors still apply.

Compare against your original source file when checking what was preserved in
the platform. The comparison labels fields as preserved, normalized, changed,
omitted or unverified; an omission from an export does not prove the value is
absent from all platform metadata. Use the exact domain FQN; it can be omitted
only when the product has exactly one domain. Comparison does not change the
platform or establish approval.

## 5. Review and create a product

For writes, change the profile to `read_only: false` and use a token with the
necessary platform privileges. Find the exact domain FQN using the domains
command above. Prepare a valid ODPS 4.1 YAML file: creation does not convert
ODPS 4.2 to 4.1. If using SDK generation, explicitly request version 4.1 with
`--odps-version 4.1` and review the generated document.

In an interactive terminal:

```sh
open-data-products openmetadata products create product.yaml --domain YOUR_DOMAIN
```

A directory can replace the file to review files recursively. The SDK checks
for duplicates and asks once before creating eligible products. Invalid files,
duplicates and incomplete duplicate checks are skipped. Visibility and
concurrent changes limit duplicate detection. Non-interactive or `--json` runs
only review; they do not create products.

For scripts, use the explicit two-step workflow:

```sh
open-data-products integrations products create openmetadata \
  --config ~/connections.yaml --source product.yaml --domain YOUR_DOMAIN --json
# Inspect the review, then use its review_sha256 with the same arguments:
open-data-products integrations products create openmetadata \
  --config ~/connections.yaml --source product.yaml --domain YOUR_DOMAIN \
  --execute --reviewed-sha256 REVIEW_SHA256 --json
```

The review binds source and destination details to its digest. It reports
mapping limitations and omissions; keep the original ODPS file. OpenMetadata's
import maps only a subset of ODPS and does not import lifecycle status. The
SDK verifies selected fields after creation; a mismatch or uncertain result
requires inspection of the destination before retrying. Writes are not
retried automatically. A digest is not business approval.

By default the authenticated account becomes owner. Use repeatable
`--owner user:NAME` or `--owner team:FQN` and `--tag CLASSIFICATION.TAG` to
choose existing platform identities and tags, or `--no-owner` with the explicit
integration command to omit the default. Assignments and linked contract import
are separate operations after product creation, so a later failure can leave the
product in place. Check the returned product ID and each outcome.

## 6. Update or delete a product

The interactive shortcuts review the target before confirmation. UUIDs are
required:

```sh
open-data-products openmetadata products update --id PRODUCT_UUID \
  --title "Revised title" --description "Revised description"
open-data-products openmetadata products delete --id PRODUCT_UUID
```

Update can also add owners and tags, or replace all current product domains
with one `--domain DOMAIN_FQN`. Review dependencies: a domain change may move
assets or detach conflicting relationships. The SDK checks the baseline and
requests revision protection, but enforcement must be verified on each server.

**Deletion is permanent and recursive** on the supported OpenMetadata 2.1.0
endpoint, and child entities may be deleted. Inspect dependencies before
confirming. For non-interactive update or deletion, first run the command to
review, then repeat the same arguments with `--execute --reviewed-sha256
REVIEW_SHA256`; deletion additionally requires `--confirm-permanent`.
Inspect the destination before retrying an uncertain write.

## 7. Domains and contracts

Create a domain with a review followed by explicit execution:

```sh
open-data-products integrations domain-create openmetadata \
  --config ~/connections.yaml --name Retail --description "Retail data" --type Aggregate
# After review, repeat with the same arguments and the returned digest:
open-data-products integrations domain-create openmetadata \
  --config ~/connections.yaml --name Retail --description "Retail data" --type Aggregate \
  --execute --reviewed-sha256 REVIEW_SHA256
```

Supported domain types are `Source-aligned`, `Consumer-aligned`, and
`Aggregate`; `--parent` accepts a parent domain FQN.

Attach one ODCS 3.1.0 YAML contract to a product that has no contract:

```sh
open-data-products integrations products contract-import openmetadata \
  --config ~/connections.yaml --id PRODUCT_UUID --source contract.yaml
# After review, repeat with the same arguments and the returned digest:
open-data-products integrations products contract-import openmetadata \
  --config ~/connections.yaml --id PRODUCT_UUID --source contract.yaml \
  --execute --reviewed-sha256 REVIEW_SHA256
open-data-products integrations products contract-get openmetadata \
  --config ~/connections.yaml --id PRODUCT_UUID --json
open-data-products integrations products contract-source openmetadata \
  --config ~/connections.yaml --id PRODUCT_UUID --output original-contract.yaml
```

This is create-only: it does not replace an existing contract. The SDK performs
basic local checks and calls the platform validation endpoint, but does not
bundle full local ODCS schema validation. On the tested 2.1.0 platform it
imports a schema-free projection and preserves the complete source as metadata;
the native contract schema is not validated as the original ODCS schema. The
preserved source can diverge from later native edits and must not contain
credentials. Inspect the review and both validation reports before execution.

## 8. Use Python

```python
from open_data_products import load_integration_config, open_integration

config = load_integration_config("/path/to/connections.yaml")
with open_integration(config.select("openmetadata")) as adapter:
    catalog = adapter.list_products_odpc()
    result = adapter.export_odps("PRODUCT_UUID")
    print("ODPS valid:", result.validation.valid)
```

The adapter's `list_products()` and `search_products()` return native paginated
results; the `*_odpc()` methods return catalogs. Consult the [SDK integration reference](https://github.com/Open-Data-Product-Initiative/odp-agent-sdk/blob/7036a9730107b357a047a78371ce6301bda89e6e/docs/integrations/openmetadata.md)
for Python write methods, error handling, detailed mapping limits and recovery
procedures.
