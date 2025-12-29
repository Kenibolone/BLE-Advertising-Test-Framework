# BLE Advertising Test Framework

This project implements a BLE advertising test framework on the ESP32-C6 to
study high-frequency advertising behavior, payload construction, and scanner-side
observation under dynamic conditions.

## Overview

The firmware repeatedly broadcasts BLE advertising packets with dynamically
generated device names at controlled intervals. The goal is to explore how BLE
advertising payloads are structured, how scanners interpret rapid advertisement
changes, and how advertising parameters affect visibility and reliability.

This project is intended for **protocol-level experimentation and learning**, not
for establishing BLE connections.

## Features

- **Dynamic Advertising Payloads**  
  Advertises dynamically generated device names to observe scanner-side behavior
  under frequent payload updates.

- **Non-connectable Advertising**  
  Uses non-connectable advertising types to focus purely on broadcast behavior.

- **Configurable Advertising Interval**  
  Advertising rate can be tuned to study timing effects and scan response limits.

## Dependencies

- ESP32 development environment (Arduino IDE with ESP32 board support)
- ESP32 Bluetooth stack:
  - `esp_bt.h`
  - `esp_gap_ble_api.h`

## Setup

### 1. Install ESP32 Board Support
- Open Arduino IDE  
- Go to **File → Preferences**  
- Add the following to **Additional Boards Manager URLs**:  
  `https://dl.espressif.com/dl/package_esp32_index.json`  
- Open **Tools → Board → Boards Manager**, search for *ESP32*, and install

### 2. Select Target Board
- **Tools → Board → XIAO ESP32C6** (or equivalent ESP32-C6 board)

### 3. Upload Firmware
- Open the source code in Arduino IDE
- Upload to the ESP32-C6

## Code Structure

### Advertising Parameters
Advertising behavior (interval, type, filtering) is configured using
`esp_ble_adv_params_t`.

### Payload Generation
A helper function generates dynamic device names and inserts them into the
advertising payload before each advertising cycle.

### GAP Callback Handling
The GAP callback handles advertisement setup completion events and triggers
advertising with updated parameters.

### Main Loop
The firmware updates the advertising payload periodically and restarts advertising
to reflect the new data.

## Usage

Once flashed, the ESP32-C6 will continuously broadcast BLE advertisements with
changing payloads. A BLE scanner (mobile app or tools like `bluetoothctl`) can be
used to observe how device names and advertisements appear over time.

## Customization

- **Advertising Interval**  
  Modify `adv_int_min` and `adv_int_max` (units of 0.625 ms) to study timing effects.

- **Advertising Payload**  
  Extend the payload to include manufacturer data or custom fields for further
  experimentation.

## Observations & Learnings

This project helped build an understanding of:
- BLE advertising packet structure
- Timing behavior and scanner response
- Limitations of frequent advertising updates
- Practical differences between theoretical BLE specs and real-world behavior

## Possible Extensions

- Support for multiple BLE advertising types
- Runtime configuration via serial input
- Comparative testing across different BLE scanners
- Logging and analysis of advertising timing behavior

## License

MIT License — see the [LICENSE](LICENSE) file for details.
