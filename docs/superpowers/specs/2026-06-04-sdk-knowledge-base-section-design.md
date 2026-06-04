# SDK Knowledge Base Section Design

## Goal

Add a dedicated SDK section to the Open Data Product Standards Knowledge Base so the repo can host the full Python SDK learning material locally. The section must make the Open Data Products Python SDK visible near the top of the knowledge base and keep imported guides organized as the material grows.

## Scope

The first implementation creates the section structure and root navigation. It does not import every existing local guide yet because those source files have not been identified inside this repo.

## Structure

- `sdk/README.md` becomes the landing page for SDK guidance.
- Future SDK guides live directly under `sdk/` with numbered filenames for learning order.
- Root `README.md` links to the SDK section from badges, quick links, the repo summary, and the tools/resources area.

## Content Model

The SDK section starts with:

- What the Open Data Products Python SDK is for.
- PyPI install link for `open-data-products`.
- Beginner-friendly setup and install path.
- Planned guide areas for ODPS validation, ODPC catalog work, ODPV vocabulary work, ODPG/generation workflows, and CLI automation.
- A note that full guide material will be imported into this repo.

## Distinction From Existing Library Entry

The Open Data Products Python SDK and the existing ODPS Python Library entry are different things. The new SDK section must not replace the ODPS Python Library entry. The tools/resources section should list both separately:

- Open Data Products Python SDK: package published on PyPI as `open-data-products`.
- ODPS Python Library: existing ODPS v4.0-focused Python library link.

## Verification

- Check Markdown links and anchor targets in `README.md`.
- Run `git diff --check`.
- Run a simple Markdown/link-oriented review with `rg` for stale wording that accidentally merges SDK and ODPS library concepts.
