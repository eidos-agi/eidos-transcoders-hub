---
name: doctor-transcoders-hub
description: Audit the Eidos Transcoders Hub for structural and quality problems. Use when a transcoder run fails the quality gate, when the run command is wrong, or before adding a new transcoder. Returns a scored health report with severity-ranked findings and copy-pasteable fixes.
---

# Doctor Transcoders Hub Contract

## Contract

```json
{
  "$schema": "https://json-schema.org/draft/2020-12",
  "title": "Transcoders Hub Health Report",
  "purpose": "Audit every transcoder skill in the hub and return a scored health report. Every finding must cite the exact transcoder and field. Every fix must be a copy-pasteable command or edit.",
  "constraints": [
    "Read every SKILL.md in skills/ before scoring",
    "Verify the run command is copy-pasteable and correct for the implementation at ~/repos-eidos-agi/transcoders/",
    "Every finding must cite transcoder name and field",
    "critical findings must have a fix",
    "Score is 0–100: start at 100, deduct per finding (critical: -20, warning: -5, info: -1)"
  ],
  "required": ["score", "status", "findings", "summary"],
  "properties": {
    "score": { "type": "number", "minimum": 0, "maximum": 100 },
    "status": { "enum": ["healthy", "needs_work", "not_ready"] },
    "findings": {
      "type": "array",
      "items": {
        "type": "object",
        "required": ["severity", "transcoder", "field", "issue", "fix"],
        "properties": {
          "severity": { "enum": ["critical", "warning", "info"] },
          "transcoder": { "type": "string" },
          "field": { "type": "string" },
          "issue": { "type": "string" },
          "fix": { "type": "string" }
        }
      }
    },
    "summary": { "type": "string" }
  }
}
```

## Audit checklist

### Contract completeness (critical if missing)
- Every transcoder SKILL.md has: `accepts`, `delivers`, `renderer`, `done_when[]`
- `renderer` names a specific free tool (reportlab, edge-tts) — not "free renderer"
- `done_when[]` has at least 3 conditions
- Run command is present and copy-pasteable

### Renderer constraint (critical if violated)
- Every renderer is free/fixed-cost — no ElevenLabs, OpenAI TTS, or paid APIs
- Renderer name matches actual implementation in `~/repos-eidos-agi/transcoders/`

### Index alignment (critical if wrong)
- Every transcoder in `skills/` is listed in `.well-known/agent-skills/index.json`
- Index descriptions match the transcoder's actual accepts/delivers
- No stale entries in the index pointing to missing skill dirs

### Quality gate coverage (warning if weak)
- `done_when` conditions are observable — not "output is good"
- At least one `not_done_when` condition exists
- Quality gate would catch a silent renderer failure

### Self-improvement (info if missing)
- `improve-transcoders-hub` skill exists and is in the index
- `doctor-transcoders-hub` skill exists and is in the index
