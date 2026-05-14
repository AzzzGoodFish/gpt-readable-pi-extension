# gpt-readable-pi-extension

A pi extension that appends communication-style instructions when the active model is GPT-like.

It activates when any of these conditions is true:

- provider is `openai`
- provider is `azure-openai`
- model id starts with `gpt-`

## Install

From GitHub:

```bash
pi install git:github.com/AzzzGoodFish/gpt-readable-pi-extension
```

For local development:

```bash
pi install /home/fish/dev/agents/gpt-readable-pi-extension
```

Or run once without installing:

```bash
pi -e /home/fish/dev/agents/gpt-readable-pi-extension
```

After installing or editing, reload pi:

```text
/reload
```

## What it does

On `before_agent_start`, the extension appends a system-prompt section covering:

- communication style
- abstraction level
- length
- expression
- collaboration behavior

The original pi system prompt is preserved. The added instructions are appended only for matching GPT models.
