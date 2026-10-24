# 05 Networking and security

Details are from general knowledge and **to verify**.

## Wi-Fi
- Home and hotspot networks (WPA2 personal) work fine on ESP32.
- Campus networks such as eduroam use WPA2-Enterprise, which is awkward. Plan to use a phone hotspot for demos.
- Captive portal networks (hotels, some venues) block the device until a browser login. Avoid.

## HTTPS (TLS)
- The MCU must verify the server certificate or the connection is not truly secure. On ESP32 this means supplying a root CA certificate or a certificate bundle. Using `setInsecure()` skips verification: fine for a throwaway test, not for the final build.
- Root certificates expire. Note the expiry of whichever one is embedded.
- The device needs correct time for certificate checks (NTP).

## API key handling
| Approach | Risk | Verdict |
|---|---|---|
| Key hard-coded in firmware | Anyone with the board or the repo can extract it | Only for private testing |
| Key in git-ignored `secrets.h` | Safe in the repo; still extractable from the board | OK for a personal demo |
| **Proxy** (Cloudflare Worker, small server) holds the key; MCU calls the proxy | Key never reaches the device; proxy can enforce the one-colour prompt, rate limits and a spending cap | Recommended |

## Proxy ideas (see `proxy/`)
- Accepts `{ "word": "..." }`, builds the system prompt server-side, calls the LLM, validates the hex, returns `{ "hex": "#RRGGBB" }`.
- Benefit: the MCU does no JSON parsing of a big reply, saving memory and making the firmware simpler.
- Protect with a simple shared token and a rate limit.
- Set a hard monthly spend limit on the API account.

## Privacy
Whatever users type is sent to a third party. Say so on the project write-up. Do not log personal data.
