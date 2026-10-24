# Parts list (proposed, 2026-10-24)

First build: four vertical tubes of about 0.5 m, so about 120 LEDs. Everything here is a **proposal**. Specs, prices and stock are unverified. Check datasheets before ordering.

| Part | Proposal | Notes |
|---|---|---|
| MCU | ESP32-S3 dev board | Wi-Fi, enough memory for HTTPS. Native USB keeps a USB keyboard possible later. Depends on open decision 1 (which board the university supplies). |
| Keyboard | Small I2C QWERTY module (M5Stack CardKB class) or a PS/2 keyboard | I2C is the simplest to code. A full-size USB keyboard needs USB host code. Depends on open decision 3. |
| Display | 128x64 OLED, 0.96" or 1.3", SSD1306 or SH1106, I2C | Shows the typed word. Shares the I2C connection with the keyboard. |
| LEDs | SK6812 RGBW addressable strip, 5V, 60 per metre | White channel gives cleaner pale colours. Pastels remain the weak point of RGB LEDs. |
| Tubes | Frosted or opal acrylic or polycarbonate tubes, 20 to 25 mm wide, about 0.5 m long | Order a sample and test with the strip. Opal diffuses more but absorbs some light. |
| Power supply | 5V DC mains adapter, 4A, barrel jack, plus a DC jack breakout | Estimate only: 120 LEDs at full white could draw several amps. Cap brightness at roughly a quarter to a third in firmware and check per-LED current on the datasheet. |
| Protection | In-line fuse (about 3A), 1000 uF capacitor across the strip power | Standard LED strip practice. |
| Data line | Level shifter (74AHCT125 class), 300 to 500 ohm resistor on each data line | 3.3V ESP32 signal to 5V strip. Some strips work without a shifter. Test. |
| Wiring | About 18 to 20 AWG for 5V and ground, thinner for data, screw terminals or connectors, perfboard | Feed power at both ends of each tube. Join all grounds. |
| Enclosure | Wooden or 3D-printed base holding the tubes upright, with a window or recess for display and keyboard | Decide early, as it sets the look. |
| Extras | USB cable for programming, reset button, optional rotary knob for brightness | |

## Alternative: ready-made DMX pixel tubes
Possible but less convenient: they need an RS-485 transceiver and DMX code, each tube needs power and a DMX connection, and the RGBW ones found have few pixels. See `research/02-display-output/sources.md`.

## Open points before ordering
1. Which MCU board does the university supply or require?
2. Built-in small keyboard, or a normal desktop keyboard plugged in?
3. How tall should the piece be? That sets tube length, LED count and power supply size.
4. Should the tubes look like stage equipment or a designed object?
