# 00 Overview

## Concept
A machine that takes a word or short phrase and answers with exactly one colour, shown on a screen or LEDs. The constraint (one colour, nothing else) is the artistic idea: a tiny "oracle" with a single-channel voice.

## Hard constraints
- Runs on an MCU, not a laptop or Raspberry Pi class computer (assumption from the brief; confirm).
- The AI cannot run on the MCU. Language models need far more memory than any MCU has, so the AI is a network call. Needs Wi-Fi.
- Reply must be machine-readable: one hex code, validated on the device.

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
| 2026-10-24 | Working assumption: ESP32 class board, hex colour reply, proxy for key | Only Wi-Fi capable, cheap, Arduino compatible option that fits the brief. Inference, not yet confirmed with owner. |

## Open questions
See "Open decisions" in the root `CLAUDE.md`.
