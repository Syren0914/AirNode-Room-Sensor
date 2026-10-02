# Hardware reference

> **Development status:** this document describes the current unfinished PCB revision. Confirm every connection against the KiCad schematic before assembly.

## Board

- Size: 70 mm × 100 mm
- Corner radius: 8 mm
- Copper layers: front and back
- Controller: ESP32-C3 SuperMini module
- Supply input: nominal 5 V through the SuperMini USB-C connector or the documented internal USB extension
- Logic voltage: 3.3 V

## ESP32-C3 pin assignment

| GPIO | Function |
| --- | --- |
| GPIO0 | TFT clock (`TFT_SCL`) |
| GPIO1 | TFT data / MOSI (`TFT_SDA`) |
| GPIO2 | TFT data/command (`DC`), with a 10 kΩ pull-up to 3.3 V |
| GPIO3 | I²C clock (`SCL`) |
| GPIO4 | I²C data (`SDA`) |
| GPIO5 | Up button |
| GPIO6 | TFT chip select (`CS`) |
| GPIO7 | TFT reset (`RST`) |
| GPIO8 | Unused in this revision |
| GPIO9 | Select button |
| GPIO10 | Back button |
| GPIO20 | Passive piezo buzzer |
| GPIO21 | Down button |

GPIO9 is a boot strapping pin on the ESP32-C3. Avoid holding Select while resetting or powering the board unless intentionally entering the associated boot state.

## Module connectors

Connector numbering follows the symbols and footprints in this repository. Check the labels printed on the module you own before plugging it in.

| Module | Pin 1 | Pin 2 | Pin 3 | Pin 4 | Pin 5 |
| --- | --- | --- | --- | --- | --- |
| TFT1 | RST | CS | DC | MOSI | SCK |
| TFT1 continued | Pin 6: GND | Pin 7: 5 V |  |  |  |
| SHT40 | SENSOR_3V3 | GND | SCL | SDA | — |
| SCD40 | SENSOR_3V3 | GND | SCL | SDA | — |
| SGP41 | SDA | SCL | GND | NC | SENSOR_3V3 |
| SPS30 | 5 V | SDA | SCL | GND | GND |

SHT40, SCD40, and SGP41 share the I²C bus. Confirm that the breakout modules contain any required pull-up resistors and that the combined pull-up resistance is suitable. Do not feed 5 V logic into the ESP32-C3 pins.

## Sensor power link

JP1 connects `SENSOR_3V3` to the board's 3.3 V rail. Install the specified insulated wire link or jumper before expecting the SHT40, SCD40, or SGP41 headers to receive power. Check for shorts before installing it.

## Buttons and alarm

SW1 through SW4 connect their GPIO signal to ground when pressed. Firmware should enable an internal pull-up for each button. BZ1 is a passive piezo element connected between GPIO20 and ground; drive it with PWM or a tone waveform. Check the selected buzzer's current requirement before direct GPIO drive. Add a transistor driver if it exceeds the ESP32-C3 GPIO rating.

## Mechanical placement

- TFT1 is positioned for the enclosure face and was moved 1 mm right and 2 mm upward from the earlier layout.
- BZ1 is mounted on the back of the PCB.
- SHT40 is on the front near the board edge for ambient-air exposure.
- SCD40 is mounted on the back with clearance from the SHT40 area.
- The module outlines still require verification with the exact purchased parts.

## USB-C programming

The SuperMini's native USB data pins are GPIO18 (D−) and GPIO19 (D+), but the current module footprint does not expose them on the header rows. The enclosure connector therefore acts as an internal USB extension to a male USB-C breakout plugged into the SuperMini. See [USB-C-extension.md](USB-C-extension.md).
