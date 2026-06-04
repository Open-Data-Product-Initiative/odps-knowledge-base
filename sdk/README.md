# Open Data Products Python SDK

The Open Data Products Python SDK is the Python package for working with the Open Data Product Standards family in code. It is published on PyPI as [`open-data-products`](https://pypi.org/project/open-data-products/).

Use this section when you want to install the SDK, validate specification files, automate standards workflows, or build applications that work with ODPS, ODPC, ODPV, and future ODPG material.

## Start here

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

## Guide map

The full SDK guide material will be imported into this repo. This page is the stable home for that material.

- **Python setup**: install Python, create a virtual environment, and understand `pip`.
- **SDK installation**: install and update `open-data-products` from PyPI.
- **ODPS workflows**: validate and work with Open Data Product Specification files.
- **ODPC workflows**: inspect and automate catalog and portfolio guidance.
- **ODPV workflows**: use controlled vocabulary terms in SDK-based workflows.
- **ODPG and generation workflows**: generate artifacts and prepare graph-oriented outputs as the standards family grows.
- **CLI automation**: use SDK commands in repeatable local and CI workflows.

## Related tools

The Open Data Products Python SDK is separate from the ODPS Python Library. The SDK covers the broader Open Data Product Standards family through the `open-data-products` package, while the ODPS Python Library remains a separate ODPS v4.0-focused library.
