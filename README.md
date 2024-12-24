# DataForge-DAQ

## Contents

This folder contains all the documents related to the DataForge-DAQ project.

## Project Aim

High-Level Design for the DAQ System

1. **Core Microcontroller/Processor**

   - Recommended Option:
     - RP2354B (dual-core Cortex-M33 or dual Hazard3 RISC-V, high performance, multiple ADC/DAC channels, SPI/QSPI support).
     - Alternatives: STM32H7 series (if additional peripherals are needed).

2. **Analog Input (16 Channels)**

   - Key Components:
     - External 24-bit ADC: **ADS1256** for high precision data acquisition.
     - Multiplexers: **2 × DG409** for flexible channel selection.
     - Programmable Gain Amplifiers: **ADA4254ACPZ** for scalable input ranges.
     - ADS1256 Channels AI4, AI5, AI6, and AI7 are left disconnected.

3. **Analog Output (8 Channels)**

   - Key Components:
     - External 16-bit DAC (e.g., DAC8568 for precision outputs).
     - Operational amplifiers (e.g., TLV2372) for buffering and output stability.

4. **Digital IO (32 Channels)**

   - Key Components:
     - Bidirectional voltage-level translators (e.g., LSF0108-Q1 for multi-voltage compatibility).
     - Direct GPIO support from the RP2354B for simple and robust design.

5. **Serial Interfaces (2 Ports)**

   - Key Components:
     - Dedicated UART transceivers (e.g., MAX3232 for RS-232, MAX485 for RS-485).

6. **CAN Interface**

   - Key Components:
     - MCP2515 SPI-based CAN controller with TJA1051 transceiver.

7. **SPI and QSPI Interfaces**

   - Key Components:
     - SPI/QSPI peripherals built into the RP2354B.
     - External SPI-based peripherals such as ADC and DAC.

8. **Networking**

   - Key Component:
     - RTL8211F Gigabit Ethernet PHY connected via RMII to the RP2354B.
     - Requires magnetics and RJ45 for Ethernet connectivity.

9. **Power Supply**

   - Requirements:
     - Wide input voltage range (e.g., 9-24V DC).
     - Voltage regulators (e.g., LM2596 for 5V, AMS1117 for 3.3V).
     - Protection circuits for overvoltage and reverse polarity.
   - Connector Types:
     - Barrel jack or pluggable terminal blocks for flexibility.

10. **Communication and Expansion**

- Communication:
  - USB Type-C for PC connectivity and power.
  - Ethernet interface (via RTL8211F).
- Expansion:
  - Pin headers for additional modules or custom features.

11. **Enclosure and Form Factor**

    - Enclosure Material: Aluminum or polycarbonate for durability.
    - Size and Layout: Compact form factor with mounting holes for DIN rails.
    - Indicators: Status LEDs for power, activity, and faults.

12. **Cost Optimization Strategies**

    - Use high-quality but low-cost components (e.g., LCSC or AliExpress for sourcing parts).
    - Modular design to allow optional features (e.g., CAN or SPI add-on boards).
    - Simplified PCB layout with 2-4 layers to minimize manufacturing costs.

## Analog Input Characteristic

- **DG409**:
  - V+ = +12V
  - V- = -12V
- **ADA4254ACPZ**:
  - VDDH = +12V
  - VDDL = -12V
  - DVDD = 3.3V
  - AVDD = 2.5V
- **ADS9234R**:
  - AVDD = 3.3V
  - DVDD = 3.3V
  ## Bandwidth Calculation for Signal Chain: AIN-DG409-ADA4254-ADS9234R

  ### Constants
  - **ADC Sampling Rate**: 3.5 MSPS (Maximum sampling rate of ADS9234R)
  - **ADC Nyquist Limit**: 1.75 MHz (Nyquist bandwidth for ADC)
  - **PGA Bandwidth**: 10 MHz (Maximum bandwidth of ADA4254 at Gain = 1)
  - **DG409 Transition Time**: 160 ns (Transition time for DG409)
  - **ADA4254 Transition Time**: 200 ns (Transition time for ADA4254)

  ### Bandwidth for Each Gain Setting
  - **Gain = 1/16**: Bandwidth = 1.75 MHz (Capped by ADC)
  - **Gain = 1/8**: Bandwidth = 1.75 MHz (Capped by ADC)
  - **Gain = 1/4**: Bandwidth = 1.75 MHz (Capped by ADC)
  - **Gain = 1/2**: Bandwidth = 1.75 MHz (Capped by ADC)
  - **Gain = 1**: Bandwidth = 1.75 MHz (Capped by ADC)
  - **Gain = 2**: Bandwidth = 1.75 MHz (Capped by ADC)
  - **Gain = 4**: Bandwidth = 1.75 MHz (Capped by ADC)
  - **Gain = 8**: Bandwidth = 1.25 MHz (PGA Limited)
  - **Gain = 16**: Bandwidth = 625 kHz (PGA Limited)
  - **Gain = 32**: Bandwidth = 312.5 kHz (PGA Limited)
  - **Gain = 64**: Bandwidth = 156.25 kHz (PGA Limited)
  - **Gain = 128**: Bandwidth = 78.125 kHz (PGA Limited)

  ### Notes
  - For Gains ≤ 1, bandwidth is capped by ADC's Nyquist limit (1.75 MHz).
  - For Gains > 1, bandwidth is limited by the PGA's frequency response.
  - Transition delays (DG409 + ADA4254) are factored into the calculation.

For **VREF = 2.5V**, **V+ = +12V**, and **V- = -12V**:

```
| Gain | Differential Input Range (±V) | Positive Input Range (0 to V) | Negative Input Range (0 to -V) | Max Bandwidth (Hz) |
|------|-------------------------------|-------------------------------|-------------------------------|--------------------|
| 1/16 | ±80.0                         | 0 to 40.0                     | 0 to -40.0                     | 1,750,000          |
| 1/8  | ±40.0                         | 0 to 20.0                     | 0 to -20.0                     | 1,750,000          |
| 1/4  | ±20.0                         | 0 to 10.0                     | 0 to -10.0                     | 1,750,000          |
| 1/2  | ±10.0                         | 0 to 5.0                      | 0 to -5.0                      | 1,750,000          |
| 1    | ±5.0                          | 0 to 2.5                      | 0 to -2.5                      | 1,750,000          |
| 2    | ±2.5                          | 0 to 1.25                     | 0 to -1.25                     | 1,750,000          |
| 4    | ±1.25                         | 0 to 0.625                    | 0 to -0.625                    | 1,750,000          |
| 8    | ±0.625                        | 0 to 0.3125                   | 0 to -0.3125                   | 1,250,000          |
| 16   | ±0.3125                       | 0 to 0.15625                  | 0 to -0.15625                  | 625,000            |
| 32   | ±0.15625                      | 0 to 0.078125                 | 0 to -0.078125                 | 312,500            |
| 64   | ±0.078125                     | 0 to 0.0390625                | 0 to -0.0390625                | 156,250            |
| 128  | ±0.0390625                    | 0 to 0.01953125               | 0 to -0.01953125               | 78,125             |
```

## License
This project is licensed under the GPLv3 License.

## Contact
For any questions or feedback, please contact:
- Email: [s.dvid@hotmail.com](mailto:s.dvid@hotmail.com)
- GitHub: [DvidMakesThings](https://github.com/DvidMakesThings)

