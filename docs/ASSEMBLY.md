# Assembly guide

This guide is for prototype assembly. The project is unfinished, so inspect the latest schematic and PCB before soldering.

## Required preparation

- Compare the purchased modules with [BOM.csv](../BOM.csv).
- Measure header pitch, board width, board length, connector overhang, and mounting holes. Similar breakout boards may use different layouts.
- Print the PCB and enclosure drawings at 100% scale or use a low-cost test PCB before committing to a full batch.
- Confirm the front/back orientation of each connector and module.

## Suggested assembly order

1. Inspect the bare PCB for shorts, incomplete milling, burrs, or damaged plating.
2. Install low-profile resistors, jumper JP1, and small connectors.
3. Check resistance between 5 V and ground and between 3.3 V and ground.
4. Install the ESP32-C3 SuperMini headers or sockets.
5. Install the TFT connector and four button switches.
6. Mount the SHT40 on the front and the SCD40 and buzzer on the back, following the PCB markings.
7. Install SGP41 and SPS30 connectors if those sensors will be used.
8. Solder `J_USB`, `R_CC1`, and `R_CC2`, then wire the illuminated latching power switch to `J_PWR` according to [USB-C-extension.md](USB-C-extension.md). Verify the switch terminals with a continuity meter because terminal positions vary by manufacturer.
9. Perform the staged tests in [BRINGUP.md](BRINGUP.md) before closing the enclosure.

## Home-milled PCB notes

- Use the widest traces and clearances that the design and cutter allow.
- Verify isolation around every pad with a magnifier and continuity meter.
- Remove copper burrs before inserting modules.
- A double-sided home-milled board does not automatically plate through-holes. Solder accessible vias on both sides or install wire rivets where required.
- Confirm that vias hidden beneath a module can be completed before mounting that module.
- Avoid relying on the solder mask shown in KiCad because a milled board may not have one.

## Sensor handling

- Keep flux, glue, conformal coating, solvents, and fingerprints away from exposed sensor openings.
- Do not place the SHT40 beside warm regulators or the ESP32 antenna area.
- Keep the SCD40 air opening unobstructed.
- Keep the SPS30 inlet and outlet paths open; it contains its own fan.
- Allow the assembled device to reach room temperature before evaluating readings.

## Enclosure installation

Dry-fit the unpowered PCB first. Confirm button travel, screen centering, USB-C insertion, wiring bend radius, buzzer clearance, and unobstructed vents. Do not force the PCB against a module or cable.
