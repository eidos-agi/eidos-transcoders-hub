---
name: podcast
description: Transcoder — convert any document (md, pdf, yaml, json) into a two-host audio discussion (MP3). Use when stakeholders need to understand a decision, report, or spec without reading it. Hosts River and Eric. Free/fixed-cost TTS only.
---

# Podcast Transcoder

Converts any substantive document → conversational two-host MP3 briefing. The listener understands the key decision, why it matters, and what changes — without having read the source.

## Run

```bash
cd ~/repos-eidos-agi/transcoders
uv run transcode.py --source <file.md|pdf|yaml> --transcoder podcast --context "<why now>"
```

## Contract

```yaml
accepts: [md, pdf, yaml, json]
delivers: MP3 audio discussion (3–10 min target ~5m)
renderer: edge-tts  # free, no API key required
voices: River (host) + Eric (expert)

done_when:
  - A non-technical executive understands every sentence on first listen
  - No rewinding needed — each idea lands before the next starts
  - Every claim maps to the source document
  - The listener can tell someone else the three key takeaways
  - Both hosts sound like people talking, not a document being read aloud

not_done_when:
  - Any sentence requires domain knowledge to parse
  - A host monologues >30s without the other reacting
  - Any number is ambiguous when spoken aloud
```

## What it decides

The transcoder decides narrative structure, which sections to cut, how to dramatize findings, and how to split dialogue. You decide what document to feed it and why now.

## Hard constraints

- Free/fixed-cost TTS only — paid APIs (ElevenLabs, OpenAI TTS) are rejected at load
- Script is persisted before rendering begins — rendering can fail, the script survives
- TTS normalization runs automatically: acronyms spaced out, numbers spoken as words, em-dashes converted to pauses

## Output

`releases/podcast/{slug}-podcast-{date}.mp3` + transcript + script
