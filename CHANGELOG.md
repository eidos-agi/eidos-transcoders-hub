# Changelog

All notable changes to eidos-transcoders-hub are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

## [1.0.0] - 2026-06-22

### Added
- `printable-report` transcoder — YAML → branded PDF via reportlab (free, no API key)
- `podcast` transcoder — any document → two-host MP3 (River + Eric) via edge-tts (free, no API key)
- `improve-transcoders-hub` skill — contract for proposing new transcoders and renderer fixes
- `doctor-transcoders-hub` skill — audits all transcoders for completeness and quality gates; scored 0–100
- Hard constraint: free/fixed-cost renderers only — paid APIs rejected at load
- `.well-known/agent-skills/index.json` for `npx skills add eidos-agi/eidos-transcoders-hub`
- `.codex-plugin/plugin.json` — Codex plugin manifest
- `.claude-plugin/plugin.json` — Claude Code plugin manifest
- `AGENTS.md` — model-agnostic orientation

### Fixed
- `printable-report`: renamed `quality_gate` → `done_when` / `not_done_when` for contract consistency
