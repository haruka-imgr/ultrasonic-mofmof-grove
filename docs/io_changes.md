# IO Definition Changes

This document describes the differences in IO (pin) definitions between this
repository and the original upstream project.

The purpose of these changes is to support a Grove-compatible hardware
configuration and external UART connections.

## Summary

- IO (pin) definitions have been modified from the upstream project
- Core algorithms and sensor processing logic are unchanged
- Changes are limited to hardware interface configuration

## Interface Comparison

### Serial Interface

| Item            | Upstream Project (USB CDC) | This Repository (Grove) |
|-----------------|----------------------------|--------------------------|
| Console type    | USB CDC                    | UART (hardware)          |
| UART instance   | N/A                        | UART0                    |
| TX pin          | N/A                        | GPIO12                   |
| RX pin          | N/A                        | GPIO13                   |
| Baud rate       | Host-controlled (logical)  | **115200 bps (physical)**|

Note: In USB CDC, the baud rate is a logical parameter provided by the host and
does not affect the actual USB transfer speed. In contrast, the UART baud rate
directly defines the physical signaling speed.

## Details

### Unchanged Interfaces

- I2C interface (SCL / SDA)  
  The I2C pin assignments are identical to the upstream project.

### Modified Interfaces

- USB CDC interface  
  The USB CDC console used in the upstream project has been replaced with a
  hardware UART interface.

- UART interface  
  Serial communication is provided via **UART0** with the following parameters:
  - TX: GPIO12  
  - RX: GPIO13  
  - Baud rate: **115200 bps**

Please refer to the source code for the exact implementation details.

## Compatibility Notes

- This firmware is **not interface-compatible** with the upstream project due
  to the change from USB CDC to UART.
- A USB serial console is no longer available.
- Ensure proper UART wiring, baud rate configuration, and voltage levels before use.

## Upstream Reference

Original project:
https://github.com/tdk-invn-oss/ultrasonic.mofmofdetection
