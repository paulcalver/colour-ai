# 02 Display and output

How a hex colour becomes light. Specs are from general knowledge, **to verify**.

## Options
| Output | How it works | Pros | Cons |
|---|---|---|---|
| Small colour TFT (ST7789, ILI9341, GC9A01 round) | SPI display; fill the screen with an RGB565 colour | Pure, flat colour; can also show the word and hex code | Needs wiring and a library (TFT_eSPI, LovyanGFX or Adafruit GFX). Backlight affects perceived colour. |
| WS2812 / NeoPixel ring, strip or matrix | One data pin, addressable RGB LEDs | Colour glows, fills a room; simple | Looks different from a screen; needs a diffuser to avoid seeing separate LEDs |
| Single RGB LED (common cathode or anode) | Three PWM pins plus resistors | Cheapest, simplest | Small; colour mixing is crude |
| E-paper | Slow refresh | Looks like paper | Colour panels have a tiny palette and take many seconds to refresh. Poor fit. |

## LED tube (current working assumption)
A vertical tube of addressable LEDs inside a frosted diffuser, showing a top to bottom gradient.

- **Gradient on an MCU:** there is no GPU, so no real shader, but none is needed. A vertical gradient depends only on position, so the firmware works out one colour per LED (or per screen row) in plain C++. Inference: for a few hundred LEDs this is trivial for an ESP32. Measure on the real board.
- **Weighting:** normalise the five weights, put each colour's centre at the middle of its share of the tube, then blend between the two nearest centres with a smoothstep curve. The demo (`demo/index.html`) implements this and can be copied.
- **Blending space:** blending in OKLab looks smoother between very different hues than plain RGB, at a small extra cost. The demo has a switch to compare.
- **Motion:** `drift` scrolls the gradient, `fade` turns each colour into the next, `pulse` swells brightness. All are cheap, since the gradient is just an array of colours. A chase effect while waiting for the API reply is an option.
- **LED type:** SK6812 RGBW strips (WS2812 style protocol plus a white LED) give cleaner pale colours than RGB. Saturated colours are good, pastels are the weak point of RGB LEDs.
- **Diffusion:** a frosted or opal tube hides the individual LEDs. Inference: 30 to 60 LEDs per metre is probably enough behind a good diffuser. Test a sample.
- **Off-the-shelf tubes:** ready-made pixel tubes exist but are mostly DMX stage lights (RGB, 11 to 88 segments; the closest RGBW match found has only 8 pixels). An ESP32 would need an RS-485 transceiver to drive them. Strips in a diffuser tube are the simpler fit. See `sources.md`.
- **Power (to verify on the datasheet):** addressable LEDs can draw a lot at full white. Use a separate 5V supply, shared ground, an in-line fuse, a capacitor across the strip power, and cap brightness in firmware. Data from a 3.3V ESP32 may need a level shifter for 5V strips.
- **Gamma:** apply gamma correction. Dim colours can look steppy on 8-bit LEDs.

## Colour handling notes
- Hex is 8 bits per channel (24-bit). Many TFTs use RGB565 (16-bit), so colours get slightly quantised.
- LEDs and screens do not display colour accurately: gamma correction matters, especially for LEDs, which look washed out without it. Inference: a simple gamma table of about 2.2 will improve the result.
- Brightness: cap NeoPixel brightness to protect the power supply and your eyes.

## Idea
Fade smoothly from the previous colour to the new one over about a second. It hides API latency and feels alive.

## Questions
- Screen, LEDs or both?
- Does the word need to be shown with the colour?
