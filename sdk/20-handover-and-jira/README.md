# Guide 20: Prepare a Handover and Deliver It to Jira

Turn a business brief into draft material for a coding assistant, review the
result, and optionally deliver it to Jira Cloud. This guide uses SDK 0.9.0.
It requires a configured LLM provider; Jira is optional for preparation.
Commands assume a POSIX shell and a project working directory.

## 1. Install and configure

```sh
python -m pip install "open-data-products==0.9.0"
open-data-products config setup
open-data-products config show
```

In an interactive terminal, setup can configure the provider and model,
OpenMetadata, Jira, and organization details. It reviews settings before
saving. Credentials entered at the hidden prompt are stored in the local `.env`;
keep it out of version control. Existing process environment variables take
precedence. `config show` displays configuration without credential values.
`open-data-products config test` tests configured services: its LLM check sends
a short prompt and may incur a charge. Connection checks do not establish
write permissions, Jira project access, or marketplace visibility.

Optionally configure a default ODPS data holder via the Organization section
of setup or `open-data-products config organization edit`. Conflicting source
values are preserved and reported; a default is not proof of ownership.

## 2. Prepare and review

Write a brief describing the business problem, desired outcomes, users,
requested fields, known constraints, and open questions. State what is unknown.
See the SDK's [business one-pager guide](https://github.com/Open-Data-Product-Initiative/odp-agent-sdk/blob/v0.9.0/docs/user/business-one-pager.md).

```sh
open-data-products handover prepare --input business-brief.md
```

Human mode is the default and requires a terminal. Review the business content
and provider destination before the first call, then the draft ODPS and
selected evidence before the next. Preparation sends reviewed content to the
provider and writes a local workspace; it does not create a Jira issue or an
OpenMetadata product. The command prints the workspace path for the next step.

The implementation draft includes OpenSpec planning artifacts, enriched ODPS,
a separate ODCS draft, mappings and open questions. Inspect the business
requirements, source evidence, proposed types, mappings, contract terms and
unresolved decisions. The SDK does not inspect the target repository or prove
that sources are accessible. A valid structure is not business approval or
implementation readiness.

For multiple briefs, provide a folder. Only top-level `.md`, `.txt` and `.docx`
files are processed, each as a separate idea. Failures do not prevent later
files from being processed, but the command exits nonzero if any fail:

```sh
open-data-products handover prepare --input briefs/ --json > results.json
```

Prompts appear on standard error; JSON on standard output lists each result and
prepared workspace. Review partial results before continuing. For optional
catalog evidence, see [Guide 21](../21-discovery-and-mcp/).

## 3. Check OpenSpec structure

OpenSpec is optional and installed separately. The SDK tested CLI 2.2.0:

```sh
npm install -g @fission-ai/openspec@2.2.0
open-data-products handover validate --input handoffs/data-product-WORKSPACE --json
```

Replace the example path with the printed workspace. The check runs in an
isolated temporary project using the SDK's default schema. `passed`, `failed`,
`incomplete`, and `not_performed` are distinct outcomes; a missing CLI is not
a pass. Review the target repository's own OpenSpec setup separately.

## 4. Deliver to Jira Cloud

Configure a named Jira connection, credentials, project and numeric issue type
ID through setup. The account needs access to the project and permission to
create the issue and upload attachments. Review the prepared workspace first:

```sh
open-data-products jira deliver --input handoffs/data-product-WORKSPACE
```

Human mode previews the issue and attachments and asks for confirmation. It
can deliver the package, source business document, enriched ODPS and ODCS draft.
Jira may require custom fields; supply a JSON file using `--fields` when needed.
Delivery can also take `results.json` from preparation or a folder of prepared
workspaces. Each issue is reviewed separately.

An issue can exist even if an attachment fails. Delivery records local results
and journals, skips confirmed deliveries on a later batch run, and stops on
unknown or incomplete outcomes. Inspect both Jira and the journal before
retrying an uncertain write.

## 5. Automate deliberately

```sh
open-data-products handover prepare --input briefs/ --mode agent > results.json
open-data-products jira deliver --input results.json --mode agent > jira-results.json
```

**Agent mode runs without interactive confirmation.** Preparation sends source
material and generated drafts to the configured provider; selected discovery
evidence may also be sent. Jira delivery creates issues and uploads attachments.
Apply your review and authorization process before invoking it. Protect result
files and workspaces, which can contain sensitive information, and handle
partial or unknown outcomes before rerunning.

See the [SDK handover reference](https://github.com/Open-Data-Product-Initiative/odp-agent-sdk/blob/v0.9.0/docs/integrations/handoff.md) for input limits, validation details, configuration, and recovery.
