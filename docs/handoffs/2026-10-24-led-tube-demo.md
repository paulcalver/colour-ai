# Handoff: LED tube concept and browser demo (2026-10-24)

Current conclusion only. Detail lives in the files linked below.

## Where the concept stands
- **Output (working assumption):** vertical tubes of addressable SK6812 RGBW LEDs inside frosted diffuser tubes, showing a weighted top to bottom gradient. Not confirmed with the owner.
- **No shader needed:** the MCU has no GPU, but a vertical gradient only depends on position, so the firmware computes one colour per LED on the CPU. Method (weights, centres, smoothstep, optional OKLab) is in `research/02-display-output/notes.md` and implemented in `demo/index.html`.
- **AI reply (under test):** JSON with up to five weighted colours plus a motion (`static`, `fade`, `drift`, `pulse`) and a tempo in seconds. One colour with `static` is still valid. The original "single colour only" brief remains the fallback.
- **Off-the-shelf tubes:** ready-made RGBW pixel tubes are mostly DMX stage fixtures with few pixels (see `research/02-display-output/sources.md`). Strips in a diffuser tube are the simpler fit for an ESP32.
- **Input and display (proposal):** small I2C keyboard plus a 128x64 I2C OLED showing the typed word.

## What exists in the repo (all on `main`)
- `demo/index.html` and `demo/README.md`: browser visualiser. Block or tube, presets, paste-a-reply, optional in-memory API key. Shows the prompt it builds and the validated reply.
- `research/04-ai-api/notes.md`: "Prompt testing" section with reply format, machine parameters, test words, what to judge, and an empty results table.
- `research/00-overview/notes.md`: decisions log entries (all marked as working assumptions).
- `hardware/parts-list.md`: proposed components, unverified.
- `CLAUDE.md`: updated architecture, open decisions and next steps.

## Not done or not verified
- **The live API call has never been run** (no key yet). The owner will add a key on desktop. If the browser blocks the request, try serving the demo locally. Default model in the demo is `claude-haiku-5-5`, editable.
- No prompt results recorded yet.
- Unverified: LED current draw, tube diffusion look, level shifter need, whether DMX tubes give four channels per pixel, OKLab matrices (typed from memory), `max_tokens` of 300 to 400 for the JSON reply, latency and cost.
- No firmware written.

## Open decisions (still the owner's)
1. Which MCU board the university supplies or requires.
2. Tube count, length, and stage-style or designed-object look.
3. Built-in small keyboard or a plugged-in desktop keyboard.
4. Direct API call from the MCU or via a proxy (proxy recommended for key safety).
5. Whether there is a written research component and its format.

## Suggested next steps
1. On desktop, add an API key, run the test words listed in `research/04-ai-api/notes.md`, and fill in the results table. Tune the system prompt in `demo/index.html` (`buildPrompt`).
2. Order a sample SK6812 strip and a frosted tube, and check diffusion and per-LED current on the datasheet.
3. Settle open decisions 1 to 3, then update `hardware/parts-list.md`.
4. Write the first firmware sketch: Wi-Fi, one API call, JSON validation (rules in `demo/index.html`), fill an LED array.

## Rules to keep
UK English, no em dashes, never commit keys or secrets, mark inference, put web facts in `sources.md`.
