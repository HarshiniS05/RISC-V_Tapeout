
---

# VSDBabySoC

**VSDBabySoC** is a small, open-source **System on Chip (SoC)** based on the **RVMYTH** RISC-V processor. It combines digital processing and analog interfacing on a single chip, integrating a **Phase-Locked Loop (PLL)** for stable clock generation and a **10-bit DAC** for converting digital signals to analog outputs. This project is designed as an educational platform for exploring SoC design and experimenting with digital-to-analog interfacing.

---

## Overview

A **System on Chip (SoC)** integrates all the main components of a computer onto a single chip. This compact design improves efficiency, reduces power consumption, and saves space—making it ideal for smartphones, wearables, IoT devices, and embedded systems.

**Key Components of an SoC include:**

* **CPU:** Handles processing and executes instructions.
* **Memory:** RAM for temporary data storage and Flash/ROM for persistent storage.
* **I/O Interfaces:** Connects the chip to external devices.
* **GPU/DSP:** Handles graphics and audio/video processing.
* **Power Management:** Optimizes energy usage.

**Advantages:** space efficiency, energy savings, faster performance, and reliability.

---

## Types of SoCs

* **Microcontroller-based:** Low-power, simple control tasks, commonly found in appliances and IoT devices.
* **Microprocessor-based:** Supports operating systems and more complex applications, suitable for smartphones and tablets.
* **Application-Specific SoCs (ASICs):** Designed for specialized tasks like AI processing or high-speed graphics.

---

## VSDBabySoC Architecture

VSDBabySoC combines three main components:

1. **RVMYTH CPU:** Executes instructions and processes digital data. It stores and updates values that the DAC uses for analog output.
2. **PLL:** Generates a stable, synchronized clock signal to coordinate the CPU and DAC, ensuring proper timing and avoiding signal mismatches.
3. **10-bit DAC:** Converts digital values from the CPU into analog signals that can drive external devices like displays or speakers.

### How It Works

* The **PLL** locks onto the input clock and provides a precise system clock.
* The **RVMYTH processor** cycles through data in its registers and prepares it for analog conversion.
* The **DAC** produces a continuous analog output based on the digital input, allowing BabySoC to interact with external analog devices.

---

## Learning Goals

VSDBabySoC is designed to:

* Provide hands-on experience with **RISC-V CPUs**.
* Demonstrate **digital-to-analog conversion** and system timing with PLLs.
* Serve as a compact, understandable example of a real SoC for educational purposes.

---

## Key Features

* Open-source and fully documented
* Small footprint, suitable for experimentation
* Supports analog output for audio/video interfaces
* Sky130-compatible design for easy fabrication

---

