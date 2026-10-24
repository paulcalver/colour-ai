# 06 Demo and presentation

## Make the demo survive a bad day
- Phone hotspot as the network, tested beforehand.
- Cached answers for a handful of likely words (sea, anger, banana, Monday) so the machine still responds if the network or API fails.
- A visible status cue (a pulsing or slowly breathing colour) while waiting for the API.
- Power from a USB power bank as a spare.

## Object design
- Diffuse LEDs behind frosted acrylic or paper; a screen alone can look like a generic gadget.
- A deliberately minimal interface suits the concept: one input, one output.
- Consider showing the word and hex code in small type, or hiding them entirely.

## Write-up angles (if a research component is needed)
- Why a single-channel reply is an interesting constraint.
- Limits of cloud dependence for an embedded object.
- Colour perception: why the same hex looks different on different outputs.
- Ethics and privacy of sending text to a third party.
- Cost and energy of calling a large model for a trivial task.

## Checklist before presenting
- [ ] Works on a different network from where it was built
- [ ] API spend limit set
- [ ] No keys or passwords in the repo
- [ ] Fallback tested with Wi-Fi off
- [ ] Parts list and wiring diagram in `hardware/`
