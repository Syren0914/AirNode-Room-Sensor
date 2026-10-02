# External USB-C extension

## Purpose

The enclosure-mounted female USB-C breakout carries USB 2.0 power and data to a short internal male USB-C breakout plugged into the ESP32-C3 SuperMini. This preserves firmware flashing and serial monitoring without modifying the SuperMini.

## Wiring

| External female breakout | Internal male breakout |
| --- | --- |
| VBUS | VBUS, through the power switch if fitted |
| GND | GND |
| D+ | D+ |
| D- | D- |
| CC1 | 5.1 kOhm to GND |
| CC2 | 5.1 kOhm to GND |

Do not tie CC1 and CC2 directly together. Each configuration-channel pin needs its own pull-down resistor for standards-compliant USB-C device detection. Keep D+ and D- short, routed together, and away from the buzzer and switching-current paths.

## Breakout dimensions and pad spacing

The enclosure model supplied for the project indicates an approximate module body envelope of 8.5 mm × 11.5 mm. Web searches found many visually similar generic 16-pin USB-C breakout boards, but they use different PCB sizes and pad arrangements. No manufacturer drawing could be matched confidently to the exact board shown in the project images.

The electrical solder-pad spacing is therefore deliberately marked **unverified**. Measure the physical breakout with calipers before creating a direct-solder PCB footprint. A generic 2.54 mm header should only be used when wires or a separate pin header connect the breakout.

## Bring-up test

1. With everything unpowered, verify VBUS, GND, D+, and D- continuity end to end.
2. Verify there is no VBUS-to-GND short.
3. Verify each CC pin measures approximately 5.1 kOhm to GND.
4. Power from a current-limited USB source.
5. Confirm the ESP32-C3 USB serial/JTAG device enumerates.
6. Test firmware flashing before closing the enclosure.
