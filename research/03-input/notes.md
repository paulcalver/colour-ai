# 03 Input

How the word gets into the machine. Single word or a few words only.

## Options
| Method | How | Pros | Cons |
|---|---|---|---|
| Phone web form served by the MCU | MCU hosts a tiny web page (own access point or on the same Wi-Fi); user types on their phone | No extra hardware; real keyboard; easy to build | Less of a self-contained object; needs a phone |
| USB keyboard | ESP32-S3 as USB host (to verify support and libraries) | Feels like a typewriter; self-contained | Only some boards; library maturity unknown |
| PS/2 keyboard | Older keyboards via two GPIO pins | Simple protocol | Hard to source |
| Serial monitor over USB | Type in the Arduino serial monitor | Zero hardware; good for development | Needs a computer connected |
| Rotary encoder with on-screen letter picker | Scroll letters, click to select | Very physical, limits input naturally | Slow; fiddly for the user |
| Small matrix keypad or button grid | Hard-wired words or letters | Reliable demo | Limited vocabulary |
| Speech | I2S microphone plus a speech-to-text API | Striking | Adds a second API, cost and complexity. Probably out of scope. |

## Suggested path
Start with the serial monitor to prove the loop, then add the phone web form. Keep a hardware input as a stretch goal.

## Design note
Limiting input length (for example 40 characters) keeps cost and latency low and reduces odd prompts.
