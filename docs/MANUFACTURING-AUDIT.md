# Manufacturing audit

Audit date: 2026-10-12

This audit covers the current KiCad sources and the PCBWay fabrication package in `manufacturing/AirNode-PCBWay-Gerbers.zip`.

## Automated results

| Check | Result |
| --- | --- |
| Schematic ERC | Pass: 0 errors and 0 warnings |
| PCB DRC | Pass: 0 violations |
| PCB connectivity | Pass: 0 unconnected pads |
| Footprint check | Pass: 0 footprint errors |
| Copper layers | F.Cu and B.Cu present |
| Board outline | 70 mm x 100 mm nominal, 8 mm corner radius |
| Gerber archive | Pass: 12 files, ZIP CRC verified |

The fabrication archive contains front and back copper, solder masks, silkscreens, Edge.Cuts, plated and non-plated drill files, drill maps, and the KiCad Gerber job file.

## USB-C input

`J_USB` is a directly soldered GCT USB4125-GF-A family receptacle using the 1.00 mm shell-stake footprint. It is placed on the back of the PCB at the lower edge. This six-contact connector provides USB-C power only; it has no D+ or D- contacts. The two CC contacts each have a 5.1 kOhm pull-down resistor.

Raw USB VBUS reaches the external latching switch header. The switched output powers the board 5 V input. Firmware flashing remains through the USB-C socket on the ESP32-C3 SuperMini module.

Use only one USB power source at a time. Do not connect separately powered cables to `J_USB` and the SuperMini USB-C socket simultaneously.

## Checks required on the first assembled board

Automated KiCad checks cannot prove physical fit or operation of purchased modules. Before ordering a larger batch:

1. Confirm the purchased USB4125 shell-stake length and pad pattern match the selected footprint.
2. Compare every breakout module's dimensions, header spacing, and pin order with the PCB.
3. Power the first board from a current-limited 5 V supply and verify the latching switch wiring before installing modules.
4. Verify the enclosure USB opening and TFT alignment against the assembled PCB.
5. Test both USB-C plug orientations, every button, the buzzer, display, and each sensor connection.
6. Run an extended thermal, Wi-Fi, sensor calibration, and airflow test inside the closed enclosure.

The Cherry MX switch footprints do not have local 3D models in the current KiCad installation. This affects the 3D preview only and does not omit their pads or holes from the fabrication files.
