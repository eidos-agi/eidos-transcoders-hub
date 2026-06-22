# Security

## Reporting

Report security issues to `hello@eidosagi.com`.

## Threat Model

- Transcoder run commands execute local processes — a malicious skill could suggest dangerous commands
- Output files are written to `releases/` — path traversal is possible if the transcoder runner doesn't validate paths
- Audio/PDF output may embed content from untrusted input documents

## Expected Controls

- All transcoder skills are reviewed before merge
- The runner (`transcoders/transcode.py`) validates `--transcoder` against an allowlist of known engines
- Free-renderer constraint prevents accidental API key exposure
- Output paths are always under `releases/` — no absolute paths allowed in skills
