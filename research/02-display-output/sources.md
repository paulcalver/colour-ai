# 02 Display and output: sources

Found 2026-10-24 by web search. Product pages may go out of stock or be retired; check before ordering.

## Addressable RGBW LEDs
- [SparkFun: Skinny LED RGBW Strip, 1m, 144 LEDs (SK6812)](https://sparkfun.com/products/14614): example SK6812 RGBW strip.
- [Enttec: SK6812 pixel protocol](https://www.enttec.com/pixel-protocols/SK6812): SK6812 is a WS2812 style chip with a white channel; 24-bit RGB or 32-bit RGBW data.
- [SK6812 RGBW datasheet (hosted by Adafruit)](https://cdn-shop.adafruit.com/product-files/2824/SJ-10030-SC-6812RGBW.pdf): read for per-LED current and timing before sizing the power supply.

## Off-the-shelf pixel tubes (DMX stage lighting)
- [JB Systems / Briteq PIXELTUBE](https://hitmusic.eu/en/product/pixeltube/): RGB, 11, 22 or 88 segments.
- [Eurolite LED PT-100/32](https://thomann.se/eurolite_led_pt_100_32_pixel_dmx_tube.htm): RGB, 32 pixels.
- [Ape Labs Neon Tube Pix](https://www.thomann.de/gr/ape_labs_neon_tube_pix.htm): RGB plus warm white, 32 pixels, rechargeable.
- [Nanlite PavoTube II 6XR](https://theasc.com/articles/nanlite-unveils-pavotube-ii-6xr): RGBWW, 8 pixels, DMX.

Not verified: whether each tube gives four channels per pixel (true RGBW control). Check the manual.

## Still to add
TFT_eSPI, LovyanGFX and Adafruit NeoPixel or FastLED library docs; datasheets for the chosen display; a gamma correction reference; an OKLab reference (Bjorn Ottosson's write-up, from which the demo's matrices were taken from memory, to verify).
