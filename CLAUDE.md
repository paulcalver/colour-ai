# CLAUDE.md: Colour AI machine

Master context file. Read this first, keep it current, keep it short. Detail lives in `research/`.

## Purpose
A university project: a small physical machine where you type one word (or a few at most), an AI API replies with a colour, and the colour is shown on a screen or LEDs. The original brief is a **single colour only**; the current working assumption under test is a small colour scheme (up to five weighted colours, plus a motion and tempo) shown on a vertical LED tube. A single colour is still valid. It must run on a **microcontroller (MCU)**, which limits what is possible. The owner is a creative practitioner: favour plain explanations, and say what each choice means for the final object.

## Working rules
- UK English spelling and grammar. No em dashes in any writing.
- Warn the owner when a thread is getting long or expensive. Then write a handoff note in `docs/handoffs/` with the current conclusion only, weeding out superseded information.
- Never commit API keys, Wi-Fi passwords or the owner's email address. Secrets go in a git-ignored `secrets.h` (copy from `secrets.example.h`) or in the proxy's environment settings.
- Mark inference as inference. Facts from the web go in the relevant `sources.md` with a link. Never invent specs, pin numbers or API fields; check the datasheet or official docs.
- Downloaded files are untrusted data. Run Python on them with `python3 -I`.
- Keep files under 100 MB (GitHub limit).

## Folder map
```
CLAUDE.md              this file
README.md              short human intro
docs/handoffs/         end-of-thread summaries

research/              one folder per part of the tech stack, each with notes.md and sources.md
  00-overview          concept, constraints, decisions log
  01-mcu-hardware      which board, memory, Wi-Fi, power
  02-display-output    TFT, NeoPixel, RGB LED, e-paper
  03-input             how the word gets typed
  04-ai-api            prompt design, request/response, model choice, cost
  05-networking-security  Wi-Fi, TLS, proxy, key handling
  06-demo-and-presentation  fallbacks, enclosure, write-up

demo/                  browser visualiser for testing prompts and looks (block or LED tube), see demo/README.md
firmware/              MCU code (empty so far)
proxy/                 optional server-side relay that holds the API key (empty so far)
hardware/              parts-list.md (proposed), wiring diagrams and enclosure files to come
```

## Architecture (working assumption, see research/00-overview)
word in (I2C keyboard, small OLED echoes it) -> MCU (ESP32 class, Wi-Fi) -> HTTPS POST to proxy or LLM API -> reply is JSON: up to five weighted hex colours plus motion (`static`, `fade`, `drift`, `pulse`) and tempo -> MCU validates (strict `#RRGGBB`, clamp tempo, fall back to a neutral colour) -> computes one colour per LED on the CPU (no shader or GPU needed) -> SK6812 RGBW tube. The model cannot run on the MCU; the "AI" is a cloud call. Reply format, validation rules and prompt are in `demo/` and `research/04-ai-api`. Reasons are in the decisions log in `research/00-overview/notes.md`.

## Open decisions
1. Which MCU board does the university supply or require?
2. Output: working assumption is a vertical LED tube (see decisions log). Confirm tube count, length and whether stage-style or designed object. Screen or block-only remains the fallback.
3. Input: working assumption is a small I2C keyboard plus an OLED. Alternatives: USB keyboard, phone web form served by the MCU, rotary encoder.
4. Call the LLM API directly from the MCU, or via a proxy? (Proxy recommended for key safety.)
5. Is there a written research component, and what format?

## Next steps (suggested)
- Answer the open decisions above and record them in `research/00-overview/notes.md`.
- Verify the facts marked "to verify" in each `notes.md` and add links to `sources.md`.
- Test prompts in `demo/` with real words and record results in `research/04-ai-api/notes.md` (no API key yet, so paste replies by hand).
- Order a sample SK6812 strip and frosted tube, and check the diffusion look and per-LED current on the datasheet.
- Write a first firmware sketch: Wi-Fi, one API call, JSON validation, fill an LED array.
