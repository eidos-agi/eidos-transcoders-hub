---
name: improve-transcoders-hub
description: Contract for proposing improvements to the Eidos Transcoders Hub. Use when a transcoder produces output that fails the quality gate, a new format transform is needed, a renderer constraint is wrong, or the run command is broken. Produces a structured proposal with copy-pasteable apply steps.
---

# Improve Transcoders Hub Contract

## Contract

```json
{
  "$schema": "https://json-schema.org/draft/2020-12",
  "title": "Transcoders Hub Improvement Proposal",
  "purpose": "Propose a specific, actionable change to the eidos-transcoders-hub — a new transcoder, a renderer fix, a quality gate update, or a constraint change. Every proposal must be motivated by an observed transcoder output that failed or a format need that isn't served.",
  "context": "Read the current transcoder skill first: skills/<name>/SKILL.md. Understand what it accepts, what it delivers, what renderer it uses, and what the quality gate requires. Check the implementation at ~/repos-eidos-agi/transcoders/. Base the proposal on what's actually there.",
  "constraints": [
    "One proposal per output",
    "observed_failure must describe a real transcoder run that went wrong or a format gap",
    "New transcoders must use a free/fixed-cost renderer — no paid API keys",
    "New transcoders require a done_when quality gate with at least 3 conditions",
    "self_update steps must be copy-pasteable"
  ],
  "required": ["observed_failure", "proposal_type", "proposal", "self_update"],
  "properties": {
    "observed_failure": {
      "type": "string",
      "description": "What transcoder output failed the quality gate, or what format need isn't served"
    },
    "proposal_type": {
      "enum": ["new_transcoder", "renderer_fix", "quality_gate_update", "constraint_change", "skill_update"]
    },
    "proposal": {
      "type": "object",
      "required": ["title", "description", "rationale"],
      "properties": {
        "title": { "type": "string" },
        "description": { "type": "string" },
        "rationale": { "type": "string" },
        "affected_transcoder": { "type": "string" },
        "renderer": { "type": "string", "description": "For new transcoders: which free renderer to use" },
        "accepts": { "type": "array", "items": { "type": "string" } },
        "delivers": { "type": "string" },
        "quality_gate": { "type": "array", "items": { "type": "string" } }
      }
    },
    "self_update": {
      "type": "object",
      "required": ["steps"],
      "properties": {
        "steps": { "type": "array", "items": { "type": "string" } },
        "verify": { "type": "string" }
      }
    }
  }
}
```

## How to apply

```bash
cd ~/repos-eidos-agi/eidos-transcoders-hub
# apply self_update.steps
git add -A && git commit -m "improve: <proposal title>"
git push
```
