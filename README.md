# ESP32 Wireless BLE Macro Pad

## Overview
A custom-engineered, rechargeable wireless macro pad designed to optimize desktop workflow and media control. Built around the **ESP32-WROOM-32**, this device acts as a Bluetooth Low Energy (BLE) Human Interface Device (HID). It requires no external drivers and interfaces natively with any host operating system.

## Hardware Architecture
* **Microcontroller:** ESP32 DevKit V1 (Dual-core, integrated Wi-Fi/BLE)
* **Power Management:** TP4056 LiPo Charging Module with onboard battery protection.
* **Inputs:** 3x Mechanical Keyswitches (multiplexed via diode matrix) & 1x EC11 Rotary Encoder.
* **Signal Routing:** Hardware debouncing and pull-up configuration for reliable state detection.

## Firmware & Software Stack
* **Environment:** C++ written via **PlatformIO**.
* **Key Libraries:** `BleKeyboard` (BLE HID Emulation), `RotaryEncoder`, `nvs_flash.h`.

## Advanced Engineering Features
* **NVS Flash Memory Management:** Implemented a long-press hardware interrupt (Switch 1 > 1000ms) that manually erases the Non-Volatile Storage (NVS) to seamlessly clear existing BLE pairing data without needing a serial connection.
* **Dynamic Profile Switching:** Firmware supports multi-layer profiling. A quick press toggles between Navigation mode (Arrow keys) and Media Control mode (Mute, Play/Pause).
* **Smart Power Monitoring:** Utilizes an analog voltage divider read by the ESP32's 12-bit ADC (Pin 33) to calculate LiPo battery percentage, which is continuously reported to the host OS via Bluetooth battery level characteristics.
* **Matrix Scanning:** Designed a custom non-blocking matrix scanning algorithm to efficiently read switch states.

## Circuit Schematic
![System Schematic](schematic.png)

## Future Revisions
* Implementation of deep-sleep modes to further extend LiPo battery life during periods of inactivity.
* Custom PCB design to transition from prototype wiring to a finalized form factor.
