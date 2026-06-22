# Contributing

Eidos Transcoders Hub is maintained by Eidos AGI and published through the Eidos marketplace.

## Adding a transcoder skill

1. Create `skills/<name>/SKILL.md` with the transcoder contract
2. Every skill must specify: `accepts`, `delivers`, `renderer`, `done_when[]`, and a copy-pasteable run command
3. Add the entry to `.well-known/agent-skills/index.json`
4. The implementation must live in `eidos-agi/transcoders` — open a PR there too

## Hard constraint

**Free/fixed-cost renderers only.** No ElevenLabs, OpenAI TTS, or any paid API. This is non-negotiable — the hub exists specifically to avoid API cost surprises.

Approved renderers: `reportlab`, `edge-tts`, `python-pptx`, `ffmpeg`, `weasyprint`.

## Standards

- `done_when[]` must have at least 3 observable conditions
- Run commands must be copy-pasteable against the actual `transcoders/` implementation
- Update CHANGELOG.md for every new transcoder or renderer change
