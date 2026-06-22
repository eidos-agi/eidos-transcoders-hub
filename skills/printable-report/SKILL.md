---
name: printable-report
description: Transcoder — render any structured YAML document as a clean, branded PDF. Use when a contract, spec, or data file needs to be reviewed, signed off, or distributed without opening a terminal.
---

# Printable Report Transcoder

Converts structured YAML → AIC-branded PDF. Faithful rendering: every field appears, nothing is truncated, no interpretation.

## Run

```bash
cd ~/repos-eidos-agi/transcoders
uv run transcode.py --source <file.yaml> --transcoder printable-report --context "<why now>"
```

## Contract

```yaml
accepts: [yaml]
delivers: branded PDF (letter, 1–4 pages)
renderer: reportlab
engine: reportlab  # free, no API key

done_when:
  - Every populated YAML field appears in the PDF
  - No field values are truncated
  - YAML comments are not rendered
  - Section headers match YAML structure

not_done_when:
  - Any YAML field is silently dropped or replaced with a placeholder
  - Output is fewer than 1 page for a non-trivial input
```

## What it decides

The transcoder decides layout, typography, and visual hierarchy. You decide content — the contract enforces faithfulness, not style.

## Output

`releases/transcoding/{slug}-contract-{date}.pdf`
