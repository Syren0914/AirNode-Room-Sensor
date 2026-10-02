# Enclosure and mechanical fit

The current enclosure is provided as [`V.2.3mf`](../V.2.3mf). It is a development model and may change with the PCB and module selection.

![AirNode enclosure prototype](images/airnode-product-angle.jpg)

## Alignment method

Use the PCB mounting holes and `Edge.Cuts` outline as the shared datum between KiCad and CAD. Import [`Room Sensor.step`](../Room%20Sensor.step) into the enclosure assembly and constrain those mounting features before adjusting openings.

For the round TFT:

1. Model the complete TFT module, including its PCB, header, display rim, and solder joints.
2. Align the module to the PCB footprint rather than centering only the visible circle.
3. Keep a small printable clearance around the display rim and test the opening with a thin front-panel slice.
4. Verify the viewing area with the screen powered before printing the full enclosure.

The current PCB places TFT1 1 mm to the right and 2 mm upward relative to the earlier layout.

## USB-C opening

The external female USB-C breakout sits near the lower edge beneath the SHT40 area and connects internally to the ESP32-C3 SuperMini. The example breakout was measured in CAD at approximately 8.5 mm × 11.5 mm, but its exact pad spacing is unverified. Measure the physical part with calipers before changing the PCB or enclosure.

Provide clearance for:

- the metal plug shell and cable overmold
- breakout-board thickness and solder joints
- the internal cable bend
- insertion force without loading the PCB

## Airflow

An additional enclosure fan is not recommended for the current design. The SPS30 includes its own airflow system, while forced air and fan heat can disturb the SHT40 and SCD40 readings. Use passive vents around the environmental sensors and keep the inlet and outlet paths open.

Keep dust out through sensible vent orientation and periodic cleaning. A dense filter can restrict particulate sampling and should only be added after measurement testing.

## Fit checklist

- PCB clears every wall, post, screw head, and wire.
- TFT is centered in the front opening.
- Buttons move freely without constant preload.
- SHT40 and SCD40 have separate, unobstructed air space.
- Buzzer does not touch the TFT or enclosure.
- USB-C plug inserts fully.
- SPS30 airflow is not recirculated.
- No vent exposes an accidental finger path to sharp solder joints.
