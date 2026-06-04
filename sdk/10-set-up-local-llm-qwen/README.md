# Guide 10: Set Up a Local LLM with Ollama and Qwen

This guide sets up a local LLM for SDK generation workflows. The SDK defaults
to Ollama on `http://localhost:11434` with the `qwen2.5` model.

## 1. Install Ollama

Install Ollama from the official installer for your operating system:

```text
https://ollama.com/download
```

After installation, start Ollama. On macOS and Windows, the desktop app usually
keeps the local server running. On Linux, start the service according to the
Ollama installation instructions.

## 2. Pull Qwen 2.5

```bash
ollama pull qwen2.5
```

This downloads the model used by the SDK default local generation workflow.

## 3. Confirm the model is available

```bash
ollama list
```

You should see a model named `qwen2.5` or `qwen2.5:latest`.

## 4. Test the local model

```bash
ollama run qwen2.5 "Write one sentence about data products."
```

If this returns text, the model is ready for local SDK generation.

## 5. Open this guide folder and create a source file

```bash
cd sdk/10-set-up-local-llm-qwen
mkdir -p source_docs fragments

cat > source_docs/turnaround-delay-signal.txt <<'TXT'
Airport operations teams need an early warning signal when aircraft turnaround
is at risk because inbound arrival is late, baggage unloading is delayed, or
the gate has a conflict.
TXT
```

## 6. Generate with the local default

```bash
open-data-products generate \
  --input source_docs/turnaround-delay-signal.txt \
  --kind signal \
  --output fragments/ \
  --json
```

The command uses the default local provider, Ollama, and the default model,
`qwen2.5`.

## 7. Override the model for one run

Use this when you have another Ollama model installed and want to try it
without editing a config file.

```bash
open-data-products generate \
  --input source_docs/turnaround-delay-signal.txt \
  --kind signal \
  --model qwen2.5 \
  --output fragments/ \
  --json
```

## Troubleshooting

- If the SDK cannot reach Ollama, confirm Ollama is running at `http://localhost:11434`.
- If the SDK says the model is missing, run `ollama pull qwen2.5` again.
- If generation is slow, try a smaller model that your machine can run comfortably and pass it with `--model`.

## What You Learned

- The SDK can generate artifacts without an online LLM provider.
- Ollama provides the local model server.
- Qwen 2.5 is the SDK default local model.
- `--model` lets you test another local model for one command.

## Next Guide

Continue to [Guide 11: Configure LLMs with a Local Config File](../11-configure-llms-with-local-config-file/).
