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
     - External 24-bit ADC 
     - Multiplexers for cost-effective channel expansion.
     - Programmable gain amplifiers for scalable input ranges.

3. **Analog Output (8 Channels)**
   - Key Components:
     - External 16-bit DAC
     - Operational amplifiers for buffering and output stability.

4. **Digital IO (32 Channels)**
   - Key Components:
     - Bidirectional voltage-level translators
     - Direct GPIO support from the RP2354B for simple and robust design.

5. **Serial Interfaces (2 Ports)**
   - Key Components:
     - Dedicated UART transceivers 

6. **CAN Interface**
   - Key Components:
     - MCP2515 SPI-based CAN controller with transceiver.

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
     - Voltage regulators 
     - Protection circuits for overvoltage and reverse polarity.
   - Connector Types:
     - Barrel jack or pluggable terminal blocks for flexibility.

10. **Communication and Expansion**
   - Communication:
     - USB Type-C for PC connectivity and power.
     - Ethernet interface (via RTL8211F).
   - Expansion:
     - Pin headers for additional modules or custom features.

11. **Cost Optimization Strategies**
    - Use high-quality but low-cost components
    - Modular design to allow optional features 
    - Simplified PCB layout with 2-4 layers to minimize manufacturing costs.

This updated setup integrates the RP2354B microcontroller for professional-grade performance while maintaining hobbyist accessibility and cost considerations. Let me know if you'd like schematics or further details on any section!

## Usage
To use the files in this project, navigate to the respective directories and follow the instructions provided in each document.

## License
This project is licensed under the GPLv3 License.

## Contact
For any questions or feedback, please contact:
- Email: [s.dvid@hotmail.com](mailto:s.dvid@hotmail.com)
- GitHub: [DvidMakesThings](https://github.com/DvidMakesThings)

