# 01 MCU hardware

All specs below are from general knowledge and are **to verify** against datasheets before relying on them.

## Needs
- Wi-Fi (the AI call is over the internet).
- Enough RAM for a TLS (HTTPS) connection. Inference: tens of KB free heap at the moment of connection.
- Enough flash for firmware plus a display library.
- Arduino or MicroPython support, so the build is quick.

## Candidates
| Board | Wi-Fi | Fit | Notes |
|---|---|---|---|
| ESP32-S3 | yes | best | Native USB, so can act as USB host for a keyboard (to verify). Plenty of RAM. |
| ESP32-C3 | yes | good | Cheap, small, single core. No USB host. |
| ESP32 (original DevKit) | yes | good | Most tutorials and libraries. |
| Raspberry Pi Pico W / Pico 2 W | yes | good | MicroPython or Arduino. HTTPS slightly fiddlier (to verify). |
| Arduino Uno / Nano (AVR) | no | not viable | No Wi-Fi, far too little RAM for TLS. |
| Arduino Nano ESP32 | yes | good | Arduino form factor with an ESP32-S3. |

## Power
- USB power is fine for a demo.
- Battery: Wi-Fi bursts draw a few hundred mA (to verify). Use a proper LiPo with a charger board, not coin cells.

## Questions
- Which board does the university supply or insist on?
- Is deep sleep or battery life a requirement? (Probably not.)
