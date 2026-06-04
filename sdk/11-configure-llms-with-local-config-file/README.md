# Guide 11: Configure LLMs with a Local Config File

Use a local generation config when you want repeatable provider, model, input,
and output settings for SDK generation. The config file belongs in your
project, not inside the installed Python package.

## 1. Copy the bundled config template

```bash
cd sdk/11-configure-llms-with-local-config-file
mkdir -p source_docs fragments

open-data-products config generation --copy-to generation.config.yaml
```

When the SDK is installed from PyPI, the bundled config is a package template.
Copy it before editing. Do not edit files under `site-packages`.

## 2. Print the selected config

```bash
open-data-products config generation \
  --config generation.config.yaml \
  --print
```

This shows the YAML the SDK will read.

## 3. Use a local Ollama config

Edit `generation.config.yaml` so the default provider is `ollama`:

```yaml
provider: ollama
model: qwen2.5
input: source_docs/
output: fragments/

providers:
  ollama:
    type: ollama
    model: qwen2.5
    baseUrl: http://localhost:11434
```

No API key is needed for local Ollama.

## 4. Add an OpenAI-compatible local server

Use `type: openai-chat` for local servers that expose
`/v1/chat/completions`, such as LM Studio, vLLM, llama.cpp server, or LocalAI.

```yaml
provider: lmstudio
model: local-model
input: source_docs/
output: fragments/

providers:
  lmstudio:
    type: openai-chat
    model: local-model
    baseUrl: http://localhost:1234/v1

  vllm:
    type: openai-chat
    model: local-model
    baseUrl: http://localhost:8000/v1
```

Replace `local-model` with the model name loaded in your local server.

## 5. Add online providers without storing secrets

Store the environment variable name in YAML, not the API key value.

```yaml
provider: openai
model: gpt-4.1-mini
input: source_docs/
output: fragments/

providers:
  openai:
    type: openai
    model: gpt-4.1-mini
    baseUrl: https://api.openai.com/v1
    apiKeyEnv: OPENAI_API_KEY

  openrouter:
    type: openai
    model: openai/gpt-4.1-mini
    baseUrl: https://openrouter.ai/api/v1
    apiKeyEnv: OPENROUTER_API_KEY

  groq:
    type: openai
    model: openai/gpt-oss-120b
    baseUrl: https://api.groq.com/openai/v1
    apiKeyEnv: GROQ_API_KEY

  claude:
    type: anthropic
    model: claude-sonnet-4-5
    baseUrl: https://api.anthropic.com/v1
    apiKeyEnv: ANTHROPIC_API_KEY
    version: "2023-06-01"
    maxTokens: 4096
```

Before selecting an online provider, export the matching key:

```bash
export OPENAI_API_KEY="your-api-key"
```

## 6. Check the config

```bash
open-data-products config generation \
  --config generation.config.yaml \
  --check
```

The check catches common key typos, missing provider or model settings,
secret-looking values, and missing configured input or prompt paths.

## 7. Generate with the config

```bash
mkdir -p source_docs fragments

cat > source_docs/turnaround-delay-signal.txt <<'TXT'
Airport operations teams need an early warning signal when aircraft turnaround
is likely to exceed planned ground time.
TXT

open-data-products generate \
  --config generation.config.yaml \
  --kind signal \
  --json
```

The command reads `input` and `output` from the config file.

## 8. Override one run from the CLI

```bash
open-data-products generate \
  --config generation.config.yaml \
  --provider ollama \
  --model qwen2.5 \
  --input source_docs/ \
  --kind signal \
  --output fragments/ \
  --json
```

CLI flags override the config for that one run.

## What You Learned

- Copy the bundled generation config before editing it.
- Local Ollama uses `type: ollama`.
- Local OpenAI-compatible servers use `type: openai-chat`.
- Online providers should store API key environment variable names, not keys.
- `--check` validates the config before generation runs.
