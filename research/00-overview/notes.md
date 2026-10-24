# 00 Overview

## Concept
A machine that takes a word or short phrase and answers with exactly one colour, shown on a screen or LEDs. The constraint (one colour, nothing else) is the artistic idea: a tiny "oracle" with a single-channel voice.

**Update 2026-10-24:** the concept is being tested in a richer form: the AI replies with up to five weighted colours plus a motion and tempo, shown on a vertical LED tube (or as a block of colour). A single colour is still valid (one colour, `static`). See `demo/` and `04-ai-api`.

## Hard constraints
- Runs on an MCU, not a laptop or Raspberry Pi class computer (assumption from the brief; confirm).
- The AI cannot run on the MCU. Language models need far more memory than any MCU has, so the AI is a network call. Needs Wi-Fi.
- Reply must be machine-readable and validated on the device. Baseline: one hex code. Under test: a small JSON colour scheme (see `04-ai-api`).

## Pipeline
1. Input (see 03-input)
2. Request to API or proxy (04-ai-api, 05-networking-security)
3. Parse and validate (04-ai-api)
4. Show colour (02-display-output)
5. Fallback if offline (06-demo-and-presentation)

## Decisions log
Add a dated line each time a decision is made.

| Date | Decision | Why |
|---|---|---|
| 2026-10-24 | Working assumption: output is a vertical tube of addressable RGBW LEDs (SK6812 type) in a frosted diffuser tube | Light spills into the room and the tube can show a weighted gradient. Off-the-shelf RGBW pixel tubes are mostly DMX stage fixtures (see `02-display-output`). Proposal, not confirmed with owner. |
| 2026-10-24 | Working assumption: reply is JSON with up to five weighted colours plus motion (`static`, `fade`, `drift`, `pulse`) and tempo | Lets the AI express a word with a gradient and movement. Firmware computes one colour per LED on the CPU, no GPU or shader needed. Being tested in `demo/`. |
| 2026-10-24 | Working assumption: keyboard on I2C and a small I2C OLED for the typed text | Few pins, simple code. See `hardware/parts-list.md`. Proposal, not confirmed with owner. |
| 2026-10-24 | Built `demo/`, a browser visualiser for block and tube output | Tests prompt and look before any hardware exists. Live API call untested (no key yet). |
| 2026-10-24 | Working assumption: ESP32 class board, hex colour reply, proxy for key | Only Wi-Fi capable, cheap, Arduino compatible option that fits the brief. Inference, not yet confirmed with owner. |

## Open questions
See "Open decisions" in the root `CLAUDE.md`.
