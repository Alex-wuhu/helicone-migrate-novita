# Novita AI — Helicone Migration Instructions for AI Agents

## TASK
You are helping a developer migrate their codebase from Helicone (an LLM proxy/gateway) to Novita AI.
Apply all changes described in this document to the target codebase automatically.
Do not ask for confirmation on changes that are unambiguous. Report a summary when done.

---

## STEP 1 — Replace Base URL

Find all occurrences of the Helicone gateway URL and replace with the Novita endpoint.

```
FIND:    https://ai-gateway.helicone.ai
REPLACE: https://api.novita.ai/openai
```

This applies to any language or configuration file: Python, TypeScript, JavaScript, .env, YAML, JSON, etc.

---

## STEP 2 — Replace API Key References

### Environment variable names
```
FIND:    HELICONE_API_KEY
REPLACE: NOVITA_API_KEY
```

Apply to: `.env`, `.env.example`, shell scripts, CI/CD config, Docker files, README, and source code.

### SDK initialization patterns

**Python**
```python
# BEFORE
OpenAI(api_key=os.environ["HELICONE_API_KEY"], base_url="https://ai-gateway.helicone.ai")
OpenAI(api_key=os.getenv("HELICONE_API_KEY"), base_url="https://ai-gateway.helicone.ai")

# AFTER
OpenAI(api_key=os.environ["NOVITA_API_KEY"], base_url="https://api.novita.ai/openai")
OpenAI(api_key=os.getenv("NOVITA_API_KEY"), base_url="https://api.novita.ai/openai")
```

**TypeScript / JavaScript**
```typescript
// BEFORE
new OpenAI({ apiKey: process.env.HELICONE_API_KEY, baseURL: "https://ai-gateway.helicone.ai" })

// AFTER
new OpenAI({ apiKey: process.env.NOVITA_API_KEY, baseURL: "https://api.novita.ai/openai" })
```

**HTTP headers**
```
FIND:    Authorization: Bearer <value of HELICONE_API_KEY>
REPLACE: Authorization: Bearer <value of NOVITA_API_KEY>
```

---

## STEP 3 — Remove Helicone-Specific Headers

Remove any HTTP headers that are Helicone-specific (they are not used by Novita and will be ignored or cause errors):

```
REMOVE these headers if present:
- Helicone-Auth
- Helicone-Cache-Enabled
- Helicone-Retry-Enabled
- Helicone-User-Id
- Helicone-Property-*  (any header starting with Helicone-Property-)
- Helicone-RateLimit-Policy
- Helicone-Target-URL
```

---

## STEP 4 — Replace Model Names

Replace all model name string values using the mapping table below.
Model names appear as the `model` parameter in API calls, config files, and constants.

### OpenAI Models

| Find (original name) | Replace (Novita name) |
|---|---|
| gpt-5.3-codex | pa/gpt-5.3-codex |
| gpt-5.2-codex | pa/gpt-5.2-codex |
| gpt-5.2-pro | pa/gpt-5.2-pro |
| gpt-5.2-chat-latest | pa/gpt-5.2-chat-latest |
| gpt-5.2 | pa/gpt-5.2 |
| gpt-5.1-codex-max | pa/gpt-5.1-codex-max |
| gpt-5.1-codex-mini | pa/gpt-5.1-codex-mini |
| gpt-5.1-codex | pa/gpt-5.1-codex |
| gpt-5.1-chat-latest | pa/gpt-5.1-chat-latest |
| gpt-5.1 | pa/gpt-5.1 |
| gpt-5-pro | pa/gpt-5-pro |
| gpt-5-codex | pa/gpt-5-codex |
| gpt-5-nano | pa/gpt-5-nano |
| gpt-5-mini | pa/gpt-5-mini |
| gpt-5-chat-latest | pa/gpt-5-chat-latest |
| gpt-5 | pa/gpt-5 |
| gpt-4.1-nano | pa/gt-4.1-n |
| gpt-4.1-mini | pa/gt-4.1-m |
| gpt-4.1 | pa/gt-4.1 |
| gpt-4o-mini | pa/gt-4p-m |
| gpt-4o | pa/gt-4p |
| o4-mini | pa/o4-mini |
| o3-mini | pa/p3-m |
| o3 | pa/p3 |
| o1-mini | pa/p1-m |
| o1 | pa/p1 |
| text-embedding-3-large | pa/text-embedding-3-large |

### Anthropic Claude Models

| Find (original name) | Replace (Novita name) |
|---|---|
| claude-opus-4-6 | pa/claude-opus-4-6 |
| claude-sonnet-4-6 | pa/claude-sonnet-4-6 |
| claude-opus-4-5-20251101 | pa/claude-opus-4-5-20251101 |
| claude-sonnet-4-5-20250929 | pa/claude-sonnet-4-5-20250929 |
| claude-haiku-4-5-20251001 | pa/claude-haiku-4-5-20251001 |
| claude-opus-4-1-20250805 | pa/claude-opus-4-1-20250805 |
| claude-sonnet-4-20250514 | pa/cd-st-4-20250514 |
| claude-opus-4-20250514 | pa/cd-op-4-20250514 |
| claude-3-7-sonnet-20250219 | pa/cd-3-7-st-20250219 |
| claude-3-5-sonnet-20241022 | pa/cd-3-5-st-20241022 |
| claude-3-5-haiku-20241022 | pa/cd-3-5-hk-20241022 |
| claude-3-haiku-20240307 | pa/cd-3-hk-20240307 |

### Google Gemini Models

| Find (original name) | Replace (Novita name) |
|---|---|
| gemini-2.5-flash-lite-preview-09-2025 | pa/gemini-2.5-flash-lite-preview |
| gemini-2.5-flash-lite-preview-06-17 | pa/gmn-2.5-fls-lt-pw-06-17 |
| gemini-2.5-flash-preview-05-20 | pa/gmn-2.5-fls-pw-05-20 |
| gemini-2.5-pro-preview-06-05 | pa/gmn-2.5-pr-pw-06-05 |
| gemini-3.1-flash-lite-preview | pa/gemini-3.1-flash-lite-preview |
| gemini-3-flash-preview | pa/gemini-3-flash-preview |
| gemini-3-pro-preview | pa/gemini-3-pro-preview |
| gemini-2.5-flash-lite | pa/gmn-2.5-fls-lt |
| gemini-2.5-flash | pa/gmn-2.5-fls |
| gemini-2.5-pro | pa/gmn-2.5-pr |
| gemini-2.0-flash-lite | pa/gmn-2.0-fls-lt |
| gemini-2.0-flash | pa/gmn-2.0-fls-20250609 |

### Grok Models

| Find (original name) | Replace (Novita name) |
|---|---|
| grok-4-1-fast-non-reasoning | pa/grok-4-1-fast-non-reasoning |
| grok-4-1-fast-reasoning | pa/grok-4-1-fast-reasoning |
| grok-4-fast-non-reasoning | pa/grok-4-fast-non-reasoning |
| grok-4-fast-reasoning | pa/grok-4-fast-reasoning |
| grok-code-fast-1 | pa/grok-code-fast-1 |
| grok-3-mini | pa/grok-3-mini |
| grok-3 | pa/grk-3 |
| grok-4 | pa/grk-4 |

> IMPORTANT: Apply longer/more-specific model names before shorter ones to avoid partial replacements.
> Example: replace `gpt-4o-mini` before `gpt-4o`, replace `gpt-5.1-codex-max` before `gpt-5.1`.

---

## STEP 5 — Update Environment Variable Files

In `.env`, `.env.example`, `.env.local`, `.env.production`, or equivalent:

```
# BEFORE
HELICONE_API_KEY=your_key_here

# AFTER
NOVITA_API_KEY=your_key_here
```

If `HELICONE_API_KEY` is also used elsewhere (not just for the LLM client), retain it and add `NOVITA_API_KEY` separately.

---

## STEP 6 — Verify

After making changes, confirm the following:
1. No remaining references to `helicone.ai` in source code or config files.
2. No remaining references to `HELICONE_API_KEY` (unless intentionally kept for other purposes).
3. All model names in API calls match a Novita model name from the tables above.
4. The `.env` file has a `NOVITA_API_KEY` entry.

Report any model names found in the codebase that do NOT appear in the mapping tables — the developer needs to contact Novita support to confirm availability.

---

## REFERENCE

- Novita API Base URL: `https://api.novita.ai/openai`
- API Key management: https://novita.ai/settings/key-management
- API is fully OpenAI-compatible (same request/response format, streaming supported)
- Anthropic prompt caching is supported via `cache_control: { type: "ephemeral" }` in message content
