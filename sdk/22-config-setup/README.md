# Guide 22: Configure the SDK

Use the guided setup in SDK 0.9.0 to configure an LLM provider, OpenMetadata,
Jira Cloud, and organization details for a project. Choose only what you need:
local validation and other non-LLM workflows do not require a provider or
platform connection.

## 1. Install and choose a project directory

Install Python and create a virtual environment first; see [Guide 0](../00-setup-python/)
if you need help. In an activated environment, install the version used here:

```sh
python -m pip install "open-data-products==0.9.0"
open-data-products --help
```

Change to the project directory where you want to keep your local configuration,
then run the following in an interactive terminal:

```sh
open-data-products config setup
```

Setup shows existing settings and lets you select the sections to configure.
It reviews the selected settings and files before saving. Read that review:
selected connection profiles may be replaced, and editing YAML can rewrite its
comments and formatting. Existing unrelated values are retained.

## 2. Choose settings for your workflow

- **LLM provider:** Choose a supported provider and model for generation and
  handover preparation. Setup can select a built-in or existing provider, or
  add a custom provider using a supported type. Remote custom URLs must use
  HTTPS; HTTP is allowed for localhost.
- **OpenMetadata:** Add a named connection to use platform discovery and
  product operations. Obtain the URL and token from your administrator; use a
  read-only connection when you only need discovery. See [Guide 19](../19-openmetadata-integration/).
- **Jira Cloud:** Add a named connection for Jira delivery. Select a project
  and numeric issue type ID available to the account. Setup can query visible
  projects and issue types, or you can enter them manually. A listed issue type
  does not guarantee permission to create an issue or satisfy required fields.
- **Organization:** Optionally enter the default ODPS data holder for generated
  drafts, including relevant contact or address details.

Credentials are entered at hidden prompts. Setup stores them in the project-local
`.env` and puts environment-variable references, rather than credential values,
in configuration YAML. Keep `.env` out of version control. Existing process
environment variables take precedence over `.env`. Generation, guided handover,
and platform CLI commands load the local file; other workflows may require
variables exported in the shell. Review project files for sensitive URLs and
personal information before sharing them.

## 3. Inspect and test

```sh
open-data-products config show
open-data-products config status --json
open-data-products config status --test
```

`show` provides a combined view without secret values. Status reports local
settings and credential presence, with next steps when something is missing.
`status --test` makes read-only OpenMetadata and Jira checks; it does not test
the LLM provider.

To test all configured, supported services, including the provider:

```sh
open-data-products config test
```

The LLM test sends a short fixed prompt and may incur provider charges. It does
not send a business document. Platform checks are read-only. A successful
check does not establish write permissions, Jira project permissions, or
marketplace visibility for other users.

## 4. Change settings later

Add, inspect, edit, or select named LLM providers:

```sh
open-data-products config llm add
open-data-products config llm list
open-data-products config llm edit --name company
open-data-products config llm use --name company
```

Replace `company` with your provider's name. Adding a provider does not select
it automatically; `use` changes the active provider after review.

Manage named OpenMetadata and Jira Cloud connections:

```sh
open-data-products config connections list
open-data-products config connections add
open-data-products config connections edit --name openmetadata
```

Replace `openmetadata` with the name to edit. Add and edit review changes
before saving; `add` does not replace an existing name. Jira project and issue
type settings are shared by guided delivery across Jira connections.

To update a credential without putting its value into shell history, use the
variable name shown by `config show` and enter the value at the hidden prompt:

```sh
open-data-products config credentials set --name OPENAI_API_KEY
```

The `.env` update is reviewed before saving. If an older value is still set in
the process environment, it takes precedence; update or remove that environment
variable as appropriate.

To review or change organization defaults:

```sh
open-data-products config organization show
open-data-products config organization edit
```

These defaults are proposals, not proof of ownership. Existing conflicting
holder values are preserved and reported for review. Organization details may
be sent to a provider as part of a later reviewed handover.

## 5. Resolve common problems

- **Command not found:** Activate the virtual environment and check that the
  SDK is installed in the same Python environment; see [Guide 0](../00-setup-python/).
- **Missing credential:** Run `config status --json`, check the variable name
  and set it through the hidden prompt. Check whether a process environment
  variable overrides the local value.
- **Provider test fails:** Check the active provider, model, endpoint and
  credential; use `config llm list` and `config show` to inspect them.
- **Platform test fails:** Check the named connection, URL, credential and
  network access with the platform administrator. A successful read-only test
  still does not establish write permissions.
- **Jira issue cannot be created:** Verify the project, numeric issue type,
  account permissions and any required custom fields. Delivery is covered in
  [Guide 20](../20-handover-and-jira/).

For exact behavior and configuration options, see the [SDK handover reference](https://github.com/Open-Data-Product-Initiative/odp-agent-sdk/blob/v0.9.0/docs/integrations/handoff.md#guided-flow).
