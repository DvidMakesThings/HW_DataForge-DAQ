# DataForge Design Specification

## Introduction

DataForge is a versatile, professional-grade Data Acquisition (DAQ) system designed to meet the needs of engineers, researchers, and hobbyists. The system combines high-performance signal acquisition and generation capabilities with cost-effective design strategies to ensure accessibility and usability.

## Design Objectives

- **Professional Performance**: High-speed, high-resolution data acquisition and generation.
- **Cost-Effectiveness**: Utilize modular and efficient designs to minimize production costs.
- **User Accessibility**: Simplified connectivity and configuration to cater to professionals and hobbyists alike.
- **Scalability**: Modular architecture to enable future expansions and customizations.

## High-Level Features

- **Analog Input**: 16+ channels with high resolution (24-bit ADC).
- **Analog Output**: 8+ channels with precision DAC.
- **Digital I/O**: 32 configurable channels for flexible interfacing.
- **Serial Interfaces**: 2 UART ports.
- **CAN Interface**: Supports industrial-standard CAN communication.
- **SPI/QSPI Interface**: High-speed data communication.
- **Integrated Connectors**: Unified connectors for serial, CAN, and SPI/QSPI interfaces.
- **Power Supply**: Wide voltage input range (9-24V DC).

## Block Diagram

The system comprises the following blocks:

- Power Supply
- Microcontroller (Core Processing Unit)
- Analog Input Subsystem
- Analog Output Subsystem
- Digital I/O Subsystem
- Communication Subsystem (Serial, CAN, SPI/QSPI)
- Expansion and Connectivity Interfaces

## Detailed Design Specifications

### 1. Core Microcontroller

- **Type**: RP2354B (Dual Cortex-M33 or Hazard3 RISC-V processors at 150 MHz).
- **Features**: Integrated 8-channel ADC, SPI/QSPI controllers, UART, and PWM for flexible control.
- **Clock Speed**: 150 MHz.
- **Operating Voltage**: 3.3V.

### 2. Analog Input Subsystem

- **Channels**: 16 differential or 32 single-ended inputs.
- **Resolution**: 24-bit ADC.
- **Programmable Gain**: Configurable for scalable input ranges using external programmable gain amplifier.
- **Input Selection**: Managed via external analog multiplexer.
- **Input Voltage Range**: Up to ±40V with programmable gain adjustment.
- **Input Protection**: Designed to limit input voltage spikes and noise for safety.

### 3. Analog Output Subsystem

- **Channels**: 8 single-ended outputs.
- **Resolution**: 16-bit DAC (DAC8568).
- **Output Voltage Range**: Configurable from 0-5V.
- **Output Buffering**: Operational amplifiers (TLV2372) for stable and accurate outputs.

### 4. Digital I/O Subsystem

- **Voltage Levels**: Selectable 3.3V or 5V logic.
- **Translator**: LSF0108-Q1 for bidirectional voltage-level shifting.
- **Protection**: Ensures safe interfacing for external connections.

### 5. Communication Subsystem

- **Serial Interfaces**:
  - 2 UART ports (RS-232 using MAX3232, RS-485 using MAX485).
- **CAN Interface**: SPI-based CAN controller (MCP2515) with TJA1051 transceiver.
- **USB**: Integrated USB 1.1 host/device controller for PC connectivity.
- **Ethernet**: RTL8211F Gigabit Ethernet PHY connected via RMII interface, requiring 25 MHz clock input.



### Pin-Level Details for DB-37 Connectors

| Pin | X1 - DIGITAL IO (DIO) | X2 - ANALOG IO (AIO) | X3 - COMMUNICATION |
|-----|------------------------|----------------------|--------------------|
| 1   | +5V                    | +5V                  | +5V                |
| 2   | GND                    | GND                  | GND                |
| 3   | DIO_0                  | AI_0                 | UART0_TX           |
| 4   | DIO_2                  | AI_2                 | UART0_DTR          |
| 5   | DIO_4                  | AI_4                 | UART0_CTS          |
| 6   | DIO_6                  | AI_6                 | GND                |
| 7   | DIO_8                  | AI_8                 | GND                |
| 8   | DIO_10                 | AI_10                | UART1_TX           |
| 9   | DIO_12                 | AI_12                | GND                |
| 10  | DIO_14                 | AI_14                | CAN_H              |
| 11  | DIO_16                 | GND                  | GND                |
| 12  | DIO_18                 | AO_0                 | QSPI_D0            |
| 13  | DIO_20                 | AO_2                 | QSPI_D2            |
| 14  | DIO_22                 | AO_4                 | QSPI_CLK           |
| 15  | DIO_24                 | AO_6                 | GND                |
| 16  | DIO_26                 | NC                   | I2C_SDA            |
| 17  | DIO_28                 | NC                   | GND                |
| 18  | DIO_30                 | NC                   | GND                |
| 19  | +3V3                   | +3V3                 | +3V3               |
| 20  | +5V                    | +5V                  | +5V                |
| 21  | GND                    | GND                  | GND                |
| 22  | DIO_1                  | AI_1                 | UART0_RX           |
| 23  | DIO_3                  | AI_3                 | UART0_DSR          |
| 24  | DIO_5                  | AI_5                 | UART0_RTS          |
| 25  | DIO_7                  | AI_7                 | UART0_DCD          |
| 26  | DIO_9                  | AI_9                 | GND                |
| 27  | DIO_11                 | AI_11                | UART1_RX           |
| 28  | DIO_13                 | AI_13                | GND                |
| 29  | DIO_15                 | AI_15                | CAN_L              |
| 30  | DIO_17                 | GND                  | GND                |
| 31  | DIO_19                 | AO_1                 | QSPI_D1            |
| 32  | DIO_21                 | AO_3                 | QSPI_D3            |
| 33  | DIO_23                 | AO_5                 | QSPI_CS            |
| 34  | DIO_25                 | AO_7                 | GND                |
| 35  | DIO_27                 | NC                   | I2C_SCL            |
| 36  | DIO_29                 | NC                   | GND                |
| 37  | DIO_31                 | NC                   | +3V3               |

### 6. Power Supply

- **Input Voltage Range**: 9-24V DC.
- **Regulators**: LM2596 for 5V, AMS1117 for 3.3V.
- **Efficiency**: Up to 90% with switch-mode regulation.
- **Protection**: Overvoltage, undervoltage, and reverse polarity protection.

### 7. Enclosure and Form Factor

- **Material**: Anodized aluminum for durability and heat dissipation.
- **Mounting**: Compatible with DIN rails and desktop use.
- **Size**: Compact form factor (150mm x 100mm x 50mm).
- **Indicators**: Multi-color LEDs for power, activity, error, and status signals.