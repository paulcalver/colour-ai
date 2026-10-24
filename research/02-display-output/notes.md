# 02 Display and output

How a hex colour becomes light. Specs are from general knowledge, **to verify**.

## Options
| Output | How it works | Pros | Cons |
|---|---|---|---|
| Small colour TFT (ST7789, ILI9341, GC9A01 round) | SPI display; fill the screen with an RGB565 colour | Pure, flat colour; can also show the word and hex code | Needs wiring and a library (TFT_eSPI, LovyanGFX or Adafruit GFX). Backlight affects perceived colour. |
| WS2812 / NeoPixel ring, strip or matrix | One data pin, addressable RGB LEDs | Colour glows, fills a room; simple | Looks different from a screen; needs a diffuser to avoid seeing separate LEDs |
| Single RGB LED (common cathode or anode) | Three PWM pins plus resistors | Cheapest, simplest | Small; colour mixing is crude |
| E-paper | Slow refresh | Looks like paper | Colour panels have a tiny palette and take many seconds to refresh. Poor fit. |

## Colour handling notes
- Hex is 8 bits per channel (24-bit). Many TFTs use RGB565 (16-bit), so colours get slightly quantised.
- LEDs and screens do not display colour accurately: gamma correction matters, especially for LEDs, which look washed out without it. Inference: a simple gamma table of about 2.2 will improve the result.
- Brightness: cap NeoPixel brightness to protect the power supply and your eyes.

## Idea
Fade smoothly from the previous colour to the new one over about a second. It hides API latency and feels alive.

## Questions
- Screen, LEDs or both?
- Does the word need to be shown with the colour?
