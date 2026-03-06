# Migrating from Helicone to Novita AI

Welcome to Novita AI. This guide helps you migrate your existing Helicone-based LLM integration to Novita in minutes. Novita provides the same OpenAI-compatible API interface, supporting all major model providers (OpenAI, Anthropic, Google Gemini, Grok) through a single unified endpoint.

---

## What Changes

| | Helicone | Novita AI |
|---|---|---|
| Base URL | `https://ai-gateway.helicone.ai` | `https://api.novita.ai/openai` |
| API Key | `HELICONE_API_KEY` | `NOVITA_API_KEY` |
| Model names | Original provider names | See model mapping table below |

That's it. Your code structure stays the same.

---

## Step-by-Step Migration

### Step 1 — Get your Novita API Key

Sign in and generate your API key at: https://novita.ai/settings/key-management

### Step 2 — Update your code

**Python (openai SDK)**

Before:
```python
from openai import OpenAI

client = OpenAI(
    api_key=os.environ["HELICONE_API_KEY"],
    base_url="https://ai-gateway.helicone.ai",
)
```

After:
```python
from openai import OpenAI

client = OpenAI(
    api_key=os.environ["NOVITA_API_KEY"],
    base_url="https://api.novita.ai/openai",
)
```

---

**TypeScript / JavaScript (openai SDK)**

Before:
```typescript
import OpenAI from "openai";

const client = new OpenAI({
  apiKey: process.env.HELICONE_API_KEY,
  baseURL: "https://ai-gateway.helicone.ai",
});
```

After:
```typescript
import OpenAI from "openai";

const client = new OpenAI({
  apiKey: process.env.NOVITA_API_KEY,
  baseURL: "https://api.novita.ai/openai",
});
```

---

**cURL**

Before:
```bash
curl https://ai-gateway.helicone.ai/chat/completions \
  -H "Authorization: Bearer $HELICONE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model": "gpt-4o", "messages": [{"role": "user", "content": "Hello"}]}'
```

After:
```bash
curl https://api.novita.ai/openai/chat/completions \
  -H "Authorization: Bearer $NOVITA_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model": "pa/gt-4p", "messages": [{"role": "user", "content": "Hello"}]}'
```

---

### Step 3 — Update model names

Novita uses its own model name identifiers. Replace the model name in your `model` parameter using the table below.

---

## Complete Model Mapping Table

### OpenAI Models

| Original Model Name | Novita Model Name | Supported Interfaces |
|---|---|---|
| gpt-5.2-codex | pa/gpt-5.2-codex | responses |
| gpt-5.3-codex | pa/gpt-5.3-codex | responses |
| gpt-5.2 | pa/gpt-5.2 | chat/completions, responses |
| gpt-5.2-chat-latest | pa/gpt-5.2-chat-latest | chat/completions, responses |
| gpt-5.2-pro | pa/gpt-5.2-pro | responses |
| gpt-5.1-codex-max | pa/gpt-5.1-codex-max | responses |
| gpt-5.1-codex-mini | pa/gpt-5.1-codex-mini | responses |
| gpt-5.1 | pa/gpt-5.1 | chat/completions, responses |
| gpt-5.1-chat-latest | pa/gpt-5.1-chat-latest | chat/completions, responses |
| gpt-5.1-codex | pa/gpt-5.1-codex | responses |
| gpt-5-pro | pa/gpt-5-pro | responses |
| gpt-5-codex | pa/gpt-5-codex | responses |
| gpt-5 | pa/gpt-5 | chat/completions, responses |
| gpt-5-mini | pa/gpt-5-mini | chat/completions, responses |
| gpt-5-nano | pa/gpt-5-nano | chat/completions, responses |
| gpt-5-chat-latest | pa/gpt-5-chat-latest | chat/completions, responses |
| gpt-4.1 | pa/gt-4.1 | chat/completions |
| gpt-4.1-nano | pa/gt-4.1-n | chat/completions |
| gpt-4.1-mini | pa/gt-4.1-m | chat/completions |
| gpt-4o | pa/gt-4p | chat/completions |
| gpt-4o-mini | pa/gt-4p-m | chat/completions |
| o1 | pa/p1 | chat/completions |
| o1-mini | pa/p1-m | chat/completions |
| o3 | pa/p3 | chat/completions |
| o3-mini | pa/p3-m | chat/completions |
| o4-mini | pa/o4-mini | chat/completions |
| text-embedding-3-large | pa/text-embedding-3-large | embeddings |

### Anthropic Claude Models

| Original Model Name | Novita Model Name | Supported Interfaces |
|---|---|---|
| claude-opus-4-6 | pa/claude-opus-4-6 | chat/completions, anthropic/v1/messages |
| claude-sonnet-4-6 | pa/claude-sonnet-4-6 | chat/completions, anthropic/v1/messages |
| claude-opus-4-5-20251101 | pa/claude-opus-4-5-20251101 | chat/completions, anthropic/v1/messages |
| claude-sonnet-4-5-20250929 | pa/claude-sonnet-4-5-20250929 | chat/completions, anthropic/v1/messages |
| claude-haiku-4-5-20251001 | pa/claude-haiku-4-5-20251001 | chat/completions, anthropic/v1/messages |
| claude-opus-4-1-20250805 | pa/claude-opus-4-1-20250805 | chat/completions, anthropic/v1/messages |
| claude-sonnet-4-20250514 | pa/cd-st-4-20250514 | chat/completions, anthropic/v1/messages |
| claude-opus-4-20250514 | pa/cd-op-4-20250514 | chat/completions, anthropic/v1/messages |
| claude-3-7-sonnet-20250219 | pa/cd-3-7-st-20250219 | chat/completions, anthropic/v1/messages |
| claude-3-5-sonnet-20241022 | pa/cd-3-5-st-20241022 | chat/completions, anthropic/v1/messages |
| claude-3-5-haiku-20241022 | pa/cd-3-5-hk-20241022 | chat/completions, anthropic/v1/messages |
| claude-3-haiku-20240307 | pa/cd-3-hk-20240307 | chat/completions, anthropic/v1/messages |

### Google Gemini Models

| Original Model Name | Novita Model Name | Supported Interfaces |
|---|---|---|
| gemini-2.5-flash | pa/gmn-2.5-fls | chat/completions, generateContent |
| gemini-2.5-pro | pa/gmn-2.5-pr | chat/completions, generateContent |
| gemini-2.5-flash-lite | pa/gmn-2.5-fls-lt | chat/completions, generateContent |
| gemini-2.0-flash | pa/gmn-2.0-fls-20250609 | chat/completions, generateContent |
| gemini-2.0-flash-lite | pa/gmn-2.0-fls-lt | chat/completions, generateContent |
| gemini-2.5-flash-preview-05-20 | pa/gmn-2.5-fls-pw-05-20 | chat/completions, generateContent |
| gemini-2.5-pro-preview-06-05 | pa/gmn-2.5-pr-pw-06-05 | chat/completions, generateContent |
| gemini-2.5-flash-lite-preview-06-17 | pa/gmn-2.5-fls-lt-pw-06-17 | chat/completions, generateContent |
| gemini-2.5-flash-lite-preview-09-2025 | pa/gemini-2.5-flash-lite-preview | chat/completions, generateContent |
| gemini-3-pro-preview | pa/gemini-3-pro-preview | chat/completions, generateContent |
| gemini-3-flash-preview | pa/gemini-3-flash-preview | chat/completions, generateContent |
| gemini-3.1-flash-lite-preview | pa/gemini-3.1-flash-lite-preview | chat/completions, generateContent |

### Grok Models

| Original Model Name | Novita Model Name | Supported Interfaces |
|---|---|---|
| grok-4-1-fast-non-reasoning | pa/grok-4-1-fast-non-reasoning | chat/completions |
| grok-4-1-fast-reasoning | pa/grok-4-1-fast-reasoning | chat/completions |
| grok-4 | pa/grk-4 | chat/completions |
| grok-4-fast-reasoning | pa/grok-4-fast-reasoning | chat/completions |
| grok-4-fast-non-reasoning | pa/grok-4-fast-non-reasoning | chat/completions |
| grok-code-fast-1 | pa/grok-code-fast-1 | chat/completions |
| grok-3 | pa/grk-3 | chat/completions |
| grok-3-mini | pa/grok-3-mini | chat/completions |

---

## Prompt Caching (Anthropic Claude)

Novita supports Anthropic prompt caching via the OpenAI-compatible interface. Use the `cache_control` field in your message content:

```json
{
  "model": "pa/cd-st-4-20250514",
  "messages": [
    {
      "role": "user",
      "content": [
        {
          "type": "text",
          "text": "<large context or system prompt>",
          "cache_control": { "type": "ephemeral" }
        },
        {
          "type": "text",
          "text": "Your question here"
        }
      ]
    }
  ]
}
```

Cache hits are reflected in the response under `prompt_tokens_details.cached_tokens`. Default cache lifetime is 5 minutes.

---

## FAQ

**Q: Do I need to change my code logic beyond the base URL, API key, and model name?**
No. Novita's API is fully OpenAI-compatible. All request/response structures remain the same.

**Q: What if my model isn't in the list?**
Contact your Novita account manager to confirm availability and enable access.

**Q: Where do I get my Novita API key?**
https://novita.ai/settings/key-management

**Q: Does Novita support streaming?**
Yes, streaming (`stream: true`) works the same way as with the OpenAI SDK.
