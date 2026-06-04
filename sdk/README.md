# Open Data Products Python SDK

The Open Data Products Python SDK is the Python package for working with the Open Data Product Standards family in code. It is published on PyPI as [`open-data-products`](https://pypi.org/project/open-data-products/).

Use this section when you want to install the SDK, validate specification files, automate standards workflows, or build applications that work with ODPS, ODPC, ODPV, and future ODPG material.

## Start Here

1. Set up Python and a virtual environment.
2. Install the SDK from PyPI.
3. Run the SDK help command.
4. Validate or inspect your first standards file.

```bash
python3 -m venv .venv-sdk
source .venv-sdk/bin/activate
python -m pip install open-data-products
open-data-products --help
```

Start with the setup guide if you have never worked with Python, `pip`, PyPI, or virtual environments before.

## Guide Package

Each guide is a self-contained folder. Open the folder, follow its `README.md`,
and use any sample files stored beside it.

### Non-LLM Guides

These guides do not require an LLM. They cover installation, validation,
explanation, vocabulary lookup, and graph conversion.

0. [Set up Python, pip, PyPI, and the SDK](00-setup-python/)
1. [Validate, explain, and summarize an ODPS product](01-validate-product/)
2. [Explain and summarize a product](02-explain-and-summarize/)
3. [Use the ODPV vocabulary helpers](03-use-vocabulary-helpers/)
4. [Convert GraphML to ODPG and open an explorer](04-convert-graph-to-odpg/)

### LLM Generation Guides

These guides use the SDK generation command. They require Ollama with Qwen 2.5
or a configured online provider.

5. [Generate one signal fragment with Ollama](05-llm-generate-one-signal/)
6. [Generate one artifact with an online provider](06-llm-use-online-provider/)
7. [Generate a full fragment set from source documents](07-llm-generate-fragment-set/)
8. [Full cycle: source docs to catalog HTML and graph explorer](08-llm-full-cycle-catalog-and-graph/)
9. [Build catalog and graph from the same fragments](09-build-catalog-and-graph-from-fragments/)
10. [Set up a local LLM with Ollama and Qwen](10-set-up-local-llm-qwen/)
11. [Configure LLMs with a local config file](11-configure-llms-with-local-config-file/)

## Related Tools

The Open Data Products Python SDK is separate from the ODPS Python Library. The SDK covers the broader Open Data Product Standards family through the `open-data-products` package, while the ODPS Python Library remains a separate ODPS v4.0-focused library.
