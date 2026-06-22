# eidos-transcoders-hub

Format pipeline transforms for AI agents. Feed a document in, get a different format out.

Transcoders are distinct from skills (no how-to) and contracts (no output schema) — they're **transforms with a registry**. Each transcoder has a contract defining what done looks like; the runner wires cognition to renderer.

## Install

```bash
npx skills add eidos-agi/eidos-transcoders-hub
```

## Transcoders

| Skill | Input | Output |
|-------|-------|--------|
| `printable-report` | yaml | Branded PDF — faithful, complete, printable |
| `podcast` | md / pdf / yaml / json | Two-host MP3 briefing — River + Eric, ~5 min |

## Run any transcoder

```bash
cd ~/repos-eidos-agi/transcoders
uv run transcode.py --source <file> --transcoder <name> --context "<why now>"
```

## Hard constraints (all transcoders)

- Free/fixed-cost renderers only — no paid API keys required
- Script persisted before rendering — rendering failures don't lose cognition output
- Quality gate must pass before output is accepted

## Source

Transcoder implementations live in [`eidos-agi/transcoders`](https://github.com/eidos-agi/transcoders). This hub is the discoverable skills index.
