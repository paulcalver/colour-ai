# 04 AI API

The "AI" part. Details here are from memory and **to verify** against the official docs before building.

## Request shape (Anthropic Messages API, to verify)
- `POST https://api.anthropic.com/v1/messages`
- Headers: `x-api-key`, `anthropic-version: 2023-06-01`, `content-type: application/json`
- Body: `model`, `max_tokens`, `system`, `messages: [{role: "user", content: "<word>"}]`
- Reply text is in `content[0].text`.

## Model choice
Use a small, fast, cheap model, since the task is trivial. Current small model ID from the session notes: `claude-haiku-5-5` (to verify availability and pricing). Any other provider with an HTTPS JSON API would also work; the firmware only needs to change its endpoint, headers and parsing.

## Prompt design
System prompt draft:

> You are a colour oracle. For any input, reply with exactly one colour as a six digit hex code in the form #RRGGBB. Output nothing else: no words, no explanation, no punctuation.

Levers:
- `max_tokens` around 10 to stop rambling and cap cost.
- Low temperature for repeatable answers; higher for more varied ones. Check which sampling parameters the chosen model accepts.
- Personality: literal, emotional, synaesthetic, or deliberately perverse. This is the creative core of the project.
- Few-shot examples in the system prompt (for example "sea" -> #1F6F8B) steer taste.

## Validation on the device (do not trust the model)
- Regex: `^#[0-9A-Fa-f]{6}$` after trimming whitespace.
- If it fails: retry once, then fall back to a default or a cached colour.
- Parse JSON with ArduinoJson (to verify memory use on the chosen board).

## Cost and latency
- A one-word prompt plus a short system prompt is a few hundred tokens at most, so cost per call should be tiny (verify against current pricing).
- Expect roughly 1 to 2 seconds round trip (inference, not measured). Measure it on the real board.

## Alternatives to explore
- Ask for a colour name and map it to hex on the device (needs a big lookup table, so probably worse).
- Constrained or structured output features, if the API offers them, to guarantee format (to verify).
- Offline fallback: a small hash-based or lookup colour generator on the MCU for when the network drops. Not AI, but keeps the demo alive.
