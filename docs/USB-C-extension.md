# Board-mounted USB-C power input

## Implemented connector

The PCB now carries `J_USB`, a GCT USB4125-03-C USB-C receptacle, on the rear lower edge. It is a six-contact, power-only receptacle with VBUS, GND, CC1, and CC2 contacts. Its footprint is `Connector_USB:USB_C_Receptacle_GCT_USB4125-xx-x_6P_TopMnt_Horizontal`.

`R_CC1` and `R_CC2` are separate 5.1 kOhm, 1% 0805 pull-downs from CC1 and CC2 to ground. Do not join the two CC pins directly.

## Latching power switch

The enclosure uses a 16 mm push-on/push-off latching switch with a 3–6 V LED ring. Wire it to `J_PWR` as follows:

| J_PWR pad | Connection |
| --- | --- |
| 1 | Raw VBUS from `J_USB` |
| 2 | Switch COM |
| 3 | Switch NO and LED+ |
| 4 | GND and LED− |

Pads 1 and 2 are linked by the PCB. When the switch latches, pad 3 receives 5 V and feeds the board `VIN (5.0v)` net. The LED ring therefore lights only while AirNode is powered. Leave the switch NC terminal unused. Verify COM, NO, NC, LED+, and LED− with the switch drawing or a continuity meter because terminal positions vary.

## Programming limitation

`J_USB` is power-only and cannot carry firmware data. The USB4125-03-C has no D+ or D− contacts, and the current ESP32-C3 SuperMini footprint does not expose its native USB pins GPIO18 and GPIO19. Program and monitor the board through the USB-C socket on the SuperMini.

## First-board checks

1. Inspect the USB shell tabs and six signal pads for solder bridges.
2. Confirm each CC pin measures approximately 5.1 kOhm to GND.
3. With the switch off, confirm `J_USB` VBUS reaches `J_PWR` pads 1 and 2 but not pad 3.
4. Latch the switch on and confirm pad 3 and ESP32 5 V receive power.
5. Confirm the LED ring polarity and that it turns off when the switch opens.
6. Test firmware flashing through the SuperMini socket before closing the enclosure.
