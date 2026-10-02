# Firmware

## Status

Firmware source has **not yet been added to this repository**. The prototype photos show working development firmware, but the project remains ongoing and unfinished. Add the source, build instructions, dependencies, and release binaries before publishing a reproducible hardware release.

## Current hardware interface

The firmware must support:

- SPI display signals on GPIO0, GPIO1, GPIO2, GPIO6, and GPIO7
- I²C sensors on GPIO3 (SCL) and GPIO4 (SDA)
- Buttons on GPIO5, GPIO21, GPIO9, and GPIO10 using pull-ups
- Passive buzzer output on GPIO20
- Wi-Fi configuration and server communication, if enabled

See [HARDWARE.md](HARDWARE.md) for the complete pin table.

## Recommended repository layout

When the firmware is published, place it in a top-level `firmware/` directory with:

- source code and configuration files
- the exact ESP32 board/core version
- dependency names and pinned versions
- build and flashing commands
- a sample configuration without secrets
- license information
- a documented data format and server endpoint configuration

Never commit Wi-Fi passwords, API keys, private certificates, or server credentials.

## Required behavior

- Detect absent sensors without locking the user interface.
- Debounce all four buttons.
- Avoid treating GPIO9 as pressed during normal boot.
- Rate-limit the buzzer and provide a way to silence alarms.
- Display a clear sensor fault when readings are unavailable or stale.
- Store calibration baselines only as recommended by each sensor manufacturer.
- Retry network operations without blocking sensor sampling or the local controls.
