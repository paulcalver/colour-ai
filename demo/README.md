# Demo: colour visualiser

A single-file browser demo for testing the concept before any hardware exists. Open `index.html` in a browser. No build step, no dependencies.

## What it does
- Shows the AI's reply as either a **block** of colour or a **vertical LED tube** (gradient, top to bottom, weighted).
- The reply is JSON with up to five weighted colours and a motion (`static`, `fade`, `drift`, `pulse`) with a tempo in seconds.
- Shows the prompt it builds, the raw reply and the validated result, so the prompt parameters can be tuned.

## Three ways to feed it
1. **Presets**: canned replies, no API key needed.
2. **Paste a reply**: paste JSON from any chat window.
3. **Ask the AI**: paste an API key into the page. It is held in memory only and never saved. Untested against the live API so far.

## Parameters set by the machine (not the user)
Output type, LED count, max colours, tempo range, white channel yes or no, input length cap. The brightness cap is applied in firmware, not requested from the AI.

## Notes
- The validation rules here (strict `#RRGGBB`, clamp tempo, truncate extra colours, fall back to a neutral grey) are the ones the firmware should copy.
- Direct browser calls expose the key to the page, so this is for private local testing only. The real build should use the proxy.
