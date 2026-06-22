# Changelog — eidos-transcoders-hub

## 2026-06-22

### Added
- `improve-transcoders-hub` skill — contract for proposing new transcoders, renderer fixes, quality gate updates
- `doctor-transcoders-hub` skill — audits all transcoders for completeness, renderer constraints, index alignment; scored 0–100
- `AGENTS.md` — model-agnostic orientation for Codex, GPT, and any agent
- `.codex-plugin/plugin.json` — hub is now a registerable Codex plugin

## 2026-06-22 (init)

### Added
- `printable-report` transcoder — YAML → branded PDF via reportlab (free, no API key)
- `podcast` transcoder — any document → two-host MP3 (River + Eric) via edge-tts (free, no API key)
- Hard constraint: free/fixed-cost renderers only — paid APIs rejected at load
- `.well-known/agent-skills/index.json` for `npx skills add eidos-agi/eidos-transcoders-hub`
