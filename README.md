# ZTH11-Zigbee-Temperature-Humidity-Sensor
Here you will find the result of my reverse engineering of a cheap Zigbee temperature & humidity sensor PCB (marking: ZTH11-ZTY-V1.2, dated 2025-10-13).  
![photo of Zigbee sensor](photos/sensor_and_package.jpg)  

---

## Schematic
Schematic of the actual PCB, drawn from visual inspection. Connections confirmed using a multimeter in continuity mode.  
KiCad project files and PDF.

## Datasheets
Datasheets for the main components, for reference.

## Photos
Photos taken before and during disassembly:  
・Sensor and its package  
・PCB top side  
・PCB top side (U3 removed)  
・PCB bottom side

## BOM
Resistor values measured in-circuit. Capacitors were desoldered and measured out-of-circuit.

## Firmware
Original firmware dumped from the ZTU module using a CH340G-based UART-to-USB adapter and [TlsrComSwireWriter](https://github.com/pvvx/TlsrComSwireWriter).

> ⚠️ The Zigbee Network Key originally found at address `0x000DC218` (16 bytes) has been replaced with a randomly generated sequence before publishing.

## Analysis

### I2C — Unknown IC ↔ CHT8310

The humidity & temperature sensor communicates over I2C with U3, an unidentified IC.  
The captured transaction sequence is documented in:  
📄 [analysis/i2c_cht8310.pdf](analysis/i2c_cht8310.pdf)

### UART — Unknown IC ↔ ZTU Module

The ZTU module communicates with the same unidentified IC over UART.  
Two captures are provided:  
- 📄 [analysis/uart_ztu_idle.pdf](analysis/uart_ztu_idle.pdf) — transactions during normal standby (without pairing)
- 📄 [analysis/uart_ztu_pairing.pdf](analysis/uart_ztu_pairing.pdf) — transactions including the full pairing sequence

## Tools & Equipment

| Purpose | Tool |
|---|---|
| Logic analysis | Saleae Logic 8 |
| Current measurement | Nordic Power Profiler Kit II (PPK2) |
| R, C measurement | LCR meter DER EE DE-5000 |

---
