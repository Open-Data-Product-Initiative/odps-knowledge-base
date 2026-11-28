# Guide 21: Metadata Discovery and MCP

SDK 0.9.0 can use read-only metadata discovery to enrich a handover with
candidate evidence, and exposes reviewed handover and Jira operations to MCP
clients. Candidates, generated mappings and plans still need human review.

## Discover evidence during preparation

First install and configure SDK 0.9.0 as described in [Guide 20](../20-handover-and-jira/).
Configure a named OpenMetadata connection with `open-data-products config setup`
or `open-data-products config connections add`. Then select that connection:

```sh
open-data-products handover prepare --input business-brief.md --discovery openmetadata
```

Replace `openmetadata` with the connection's actual name. The default connection
file is `connections.yaml`; use `--connections PATH` for another file. Without
`--discovery`, preparation skips this step. OpenMetadata is the first implemented
discovery adapter; other platforms require an implemented adapter.

The SDK proposes source-backed search concepts, searches a bounded set of
metadata, and inspects candidate products, assets, schemas, contracts and
one-hop lineage where available. Search is lexical and bounded; matches can be
wrong or incomplete. The snapshot records provenance and incomplete requests,
and the handover includes supporting evidence and a credential-free platform
origin. Review the candidate columns and provider preview before confirmation.
A snapshot can contain sensitive metadata even without credentials.

The retained snapshot is limited to 1 MiB and provider asset evidence to 256 KiB;
exceeding a budget fails the affected document rather than silently sending an
oversized snapshot. Failure or unavailability of discovery can leave preparation
without catalog evidence. Confirm access, schema details and mappings independently.

For a separate product discovery request, use its platform UUID:

```sh
open-data-products openmetadata discover --id PRODUCT_UUID --json
```

See [Guide 19](../19-openmetadata-integration/) for connection setup and the
[SDK handover reference](https://github.com/Open-Data-Product-Initiative/odp-agent-sdk/blob/v0.9.0/docs/integrations/handoff.md) for discovery limits and evidence details.

## Connect an MCP client

Start the SDK's stdio MCP server from an MCP-capable client using the executable
and arguments below. The client must use a project directory with the necessary
configuration and credentials; consult its documentation for server setup.

```text
open-data-products serve
```

Do not treat all MCP tools as read-only. The client can discover the tool schemas
and classifications via MCP. For a handover, the intended sequence is:

1. Call `preview_business_handover`, review source and provider, then call
   `create_business_odps_draft` with the same inputs and review digest.
2. Call `preview_implementation_handover` with the staged business document,
   ODPS draft, new output directory and change name. Review it and call
   `create_implementation_handover` with the same inputs and digest. An optional
   `context_file` supplies an existing metadata snapshot.
3. For Jira, call `review_jira_handover`, review the issue, destination and
   attachments, then call `deliver_jira_handover` with the matching digest and
   a new local journal file. The general-issue equivalents are
   `review_jira_issue` and `create_jira_issue`.

Generation can send content to a provider and write local files; delivery can
create an issue and upload attachments. Existing journals block retries. Check
Jira and the journal after an unknown or partial result. MCP package generation
accepts an existing snapshot but does not run automatic metadata discovery.
See the [MCP workflow reference](https://github.com/Open-Data-Product-Initiative/odp-agent-sdk/blob/v0.9.0/docs/integrations/handoff.md#mcp-tools) for inputs and delivery methods.
