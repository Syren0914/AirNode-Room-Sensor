# Prototype bring-up

Use a current-limited bench supply when possible. Stop if a component heats unexpectedly or the supply immediately reaches its current limit.

## 1. Unpowered checks

- Inspect both copper layers for bridges and incomplete isolation.
- Check continuity from each supply pin to its intended rail.
- Confirm there is no short from 5 V to ground or 3.3 V to ground.
- Confirm JP1 is installed only after the sensor rail has been checked.
- Check that each button shorts its signal to ground only while pressed.

## 2. Controller-only power test

1. Remove plug-in sensor modules if sockets are used.
2. Apply 5 V with a conservative current limit.
3. Verify the board's 3.3 V rail before fitting sensors.
4. Confirm the ESP32-C3 can be detected and programmed through its internal USB connection.
5. Disconnect power and investigate any abnormal current or heating.

## 3. Peripheral tests

Add and test one subsystem at a time:

1. TFT: verify reset, chip select, command/data, clock, and MOSI.
2. Buttons: verify Up, Down, Select, and Back individually. Remember that Select uses GPIO9.
3. Buzzer: begin with a short, low-duty PWM tone.
4. SHT40: scan the I²C bus, then compare temperature and humidity with a reference.
5. SCD40: allow warm-up and verify plausible CO₂ readings in fresh indoor air.
6. SGP41: follow the sensor library's conditioning and compensation requirements.
7. SPS30: verify clear inlet/outlet airflow and plausible particulate readings.

## 4. Enclosure test

- Run the assembled unit with the cover installed and log readings over several hours.
- Compare covered and uncovered SHT40 temperature to detect self-heating.
- Check that SCD40 readings respond when occupied air reaches the vents.
- Check that the SPS30 exhaust does not recirculate directly into its inlet.
- Confirm that the external USB-C port supports both power and programming in both plug orientations.

## 5. Release checks still required

Before calling a revision complete, record the tested module part numbers, verify enclosure tolerances, repeat ERC/DRC, test every manufactured board, validate sensor calibration, and perform long-duration power and thermal testing.
