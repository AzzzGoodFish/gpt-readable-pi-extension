# gpt-readable-pi-extension

A pi extension that makes GPT-like models communicate from high-level signal first.

The goal is not to make replies longer or more polished. The goal is to make them easier to understand by prioritizing higher-level information before details: conclusion before explanation, structure before implementation, diagnosis before commands, and decisions before mechanics.

## Philosophy

GPT models often answer by immediately expanding into details, alternatives, or implementation steps. That can be useful, but it can also bury the important point.

This extension nudges the model to communicate in this order:

1. Start with the conclusion.
2. Explain the structure, trade-offs, or diagnosis.
3. Drop into concrete details only when needed.

This is especially useful for coding-agent work, where the user usually needs orientation first and implementation detail second.

## Behavior

When active, the extension appends communication instructions to pi's system prompt covering:

- conclusion-first answers
- high-level abstraction before implementation detail
- concise response length
- short paragraphs and brief code blocks
- direct, non-hedged judgments
- collaboration where the user remains the decision-maker

The original pi system prompt is preserved. The added instructions are appended only for matching GPT models.

## Activation

The extension activates when any of these conditions is true:

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

## How it works

The extension listens to pi's `before_agent_start` event. If the active model matches the GPT conditions, it returns a modified system prompt:

```ts
systemPrompt: `${event.systemPrompt}\n\n${communicationStylePrompt}`
```

This affects the current model turn without modifying pi's built-in prompt files.
