# External USB-C extension

## Purpose

The enclosure-mounted female USB-C breakout carries USB 2.0 power and data to a short internal male USB-C breakout plugged into the ESP32-C3 SuperMini. This preserves firmware flashing and serial monitoring without modifying the SuperMini.

## Wiring

| External female breakout | Internal male breakout |
| --- | --- |
| VBUS | Switch COM; switch NO then connects to internal VBUS |
| GND | GND |
| D+ | D+ |
| D- | D- |
| CC1 | 5.1 kOhm to GND |
| CC2 | 5.1 kOhm to GND |

Do not tie CC1 and CC2 directly together. Each configuration-channel pin needs its own pull-down resistor for standards-compliant USB-C device detection. Keep D+ and D- short, routed together, and away from the buzzer and switching-current paths.

## Latching illuminated power switch

The enclosure uses a 16 mm push-on/push-off latching switch with a 3–6 V LED ring. It is an off-board, wired component. Only the USB 5 V VBUS conductor passes through the switching contacts:

```text
External USB-C VBUS -> switch COM
Switch NO           -> internal male USB-C VBUS
External USB-C GND  -> internal GND and switch LED-
Switch NO           -> switch LED+
External D+         -> internal D+
External D-         -> internal D-
```

With this wiring, one press latches the contacts closed and powers AirNode; the next press opens them and turns it off. Connecting LED+ to the switched side makes the ring illuminate only while AirNode is on. Ground and the USB data lines remain continuous and are not switched.

The terminal arrangement is not standardized. Identify COM, NO, NC, LED+, and LED- from the supplied diagram or with a continuity meter before wiring. Leave NC unused. Confirm that the contact rating safely exceeds the complete device's measured 5 V current.

### KiCad PCB connection: J_PWR

The back of the PCB now includes the four-pin `J_PWR` wiring header:

| J_PWR pad | Connect to |
| --- | --- |
| 1 | External USB-C VBUS |
| 2 | Latching switch COM |
| 3 | Latching switch NO and LED+ |
| 4 | External USB-C GND and LED− |

Pads 1 and 2 are connected by a wide raw-VBUS trace. Pad 3 feeds the board's `VIN (5.0v)` net only after the switch latches closed. Pad 4 connects to board ground. USB D+ and D− still run directly between the external female and internal male USB-C breakouts because the SuperMini module does not expose GPIO18 and GPIO19 on its headers.

## Breakout dimensions and pad spacing

The enclosure model supplied for the project indicates an approximate module body envelope of 8.5 mm × 11.5 mm. Web searches found many visually similar generic 16-pin USB-C breakout boards, but they use different PCB sizes and pad arrangements. No manufacturer drawing could be matched confidently to the exact board shown in the project images.

The electrical solder-pad spacing is therefore deliberately marked **unverified**. Measure the physical breakout with calipers before creating a direct-solder PCB footprint. A generic 2.54 mm header should only be used when wires or a separate pin header connect the breakout.

## Bring-up test

1. With everything unpowered, verify VBUS, GND, D+, and D- continuity end to end.
2. Verify there is no VBUS-to-GND short.
3. Verify each CC pin measures approximately 5.1 kOhm to GND.
4. Power from a current-limited USB source.
5. Confirm that one press latches power on, the LED ring illuminates, and the next press removes power.
6. Confirm the ESP32-C3 USB serial/JTAG device enumerates while the switch is on.
7. Test firmware flashing before closing the enclosure.
