# Eidos Transcoders Hub — Agent Orientation

You are an agent working in the Eidos Transcoders Hub repository.

## What this repo is

A skill registry for **format pipeline transforms**. Feed a document in, get a different format out. Each transcoder has a contract defining what done looks like; the runner wires cognition to renderer.

Transcoders are distinct from:
- Skills (no how-to procedure here — just the contract and run command)
- Contracts (no output schema — the output is a file, not JSON)

## Key files

- `skills/` — one directory per transcoder, each with `SKILL.md`
- `.well-known/agent-skills/index.json` — discoverable via `npx skills add`
- `.codex-plugin/plugin.json` — Codex plugin manifest

## Transcoders available

| Name | Input | Output | Renderer |
|------|-------|--------|----------|
| `printable-report` | yaml | Branded PDF | reportlab (free) |
| `podcast` | md / pdf / yaml / json | Two-host MP3 | edge-tts (free) |

## Hard constraint

Free/fixed-cost renderers only. No paid API keys required or accepted.

## Running a transcoder

```bash
cd ~/repos-eidos-agi/transcoders
uv run transcode.py --source <file> --transcoder <name> --context "<why now>"
```

Implementations live in `eidos-agi/transcoders`. This hub is the discoverable index.

## Install

```bash
npx skills add eidos-agi/eidos-transcoders-hub
```
