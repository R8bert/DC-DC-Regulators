# ME3116 40V, 1.0A Step-Down Converter PCB

This repository contains the hardware design files for a compact, high-efficiency DC-DC step-down (buck) converter based on the ME3116 integrated circuit.

This PCB is designed to take a wide input voltage (4.75V to 40V) and convert it to a stable, lower output voltage with a continuous current capacity of up to 1.0A. The 550KHz switching frequency allows for the use of small external components, and its wide input range makes it suitable for power conditioning from unregulated sources.

## Key Features

* **Wide Input Voltage Range:** 4.75V to 40V
* **Continuous Output Current:** 1.0A
* **High Efficiency:** Up to 90%, with high light-load efficiency via **PWM/PFM switching**.
* **Switching Frequency:** 550KHz fixed frequency.
* **Low Shutdown Current:** Approximately 0.7µA typical.
* **Internal Compensation:** Reduces external component count and design complexity.
* **Internal Protections:** Includes Short Circuit Protection (Frequency Foldback), Thermal Shutdown (TSD), and VIN Under-Voltage Lockout (UVLO).
* **Compact Footprint:** Based on the SOT23-6 package.

## Technical Specifications

| Parameter | Value | Notes |
| :--- | :--- | :--- |
| **Integrated Circuit** | ME3116 | |
| **Input Voltage (Vin)** | 4.75V – 40V |
| **Output Voltage (Vout)** | Configurable | Set by feedback resistors RF/RG. |
| **Max Output Current** | 1.0A | 1.2A Peak SW Current Limit |
| **Switching Frequency** | 550KHz | Fixed (PWM Operation) |
| **Feedback Voltage (Vref)** | 0.8V (Typical) | |
| **Quiescent Current** | \~1.35mA (Switching, No Load) | \~0.7µA (Shutdown) |
| **Topology** | Asynchronous Buck | Requires an external Schottky diode. |
| **Protections** | OCP, TSD, SCP, UVLO | |

## Connections and Pinout

* **VIN+**: Positive input voltage (4.75V to 40V)
* **GND**: Common ground for input and output
* **VOUT+**: Regulated positive output voltage
* **VOUT-**: Common ground for input and output


## Output Voltage Configuration

The output voltage (Vout) is set by the resistive divider formed by RF (top resistor) and RG (bottom resistor), connecting VOUT to the FB (Feedback) pin. The ME3116 regulates the FB pin to a reference voltage (Vref) of **0.8V**.

The output voltage is calculated using the following formula:

$$
V_{out} = 0.8V \times (1 + \frac{RF}{RG})
$$

To calculate the resistor values (datasheet recommends RG in the 100Ω - 10kΩ range):

$$
RF = RG \times (\frac{V_{out}}{0.8V} - 1)
$$

**Example:** For a 5V output, using RG = 10kΩ:
* `RF = 10kΩ * (5.0V / 0.8V - 1)`
* `RF = 10kΩ * (6.25 - 1)`
* `RF = 10kΩ * 5.25`
* `RF = 52.5kΩ`
* Use the nearest standard 1% resistor value: **52.3kΩ**. This will produce `Vout = 0.8V * (1 + 52.3k/10k) = 4.984V`.

### Common Voltage Settings

Here are suggested 1% standard resistor values for common output voltages.

| Target Vout | RF (Top Resistor) | RG (Bottom Resistor) | Calculated Vout |
| :--- | :--- | :--- | :--- |
| 1.8V | 12.5kΩ | 10kΩ | 1.800V |
| 2.5V | 21.0kΩ | 10kΩ | 2.480V |
| 3.3V | 31.6kΩ | 10kΩ | 3.328V |
| 5.0V | 52.3kΩ | 10kΩ | 4.984V |
| 9.0V | 20.5kΩ | 2kΩ | 9.000V |
| 12.0V | 28.0kΩ | 2kΩ | 12.000V |

---

## Schematic

<img width="617" height="313" alt="image" src="https://github.com/user-attachments/assets/37b835c2-73e9-4136-aac2-2e5153c11835" />


## PCB 

! I need to upload some images !!! 

## Bill of Materials (BOM)

[Check this html](https://github.com/R8bert/DC-DC-Regulators/blob/main/Buck%20Converter%20(Step%20Down)/ME3116/ibom.html "Interactive BOM - ME3116")

## Design Files

This project was designed using `[KiCad]`.

All original design files (schematic, PCB layout, Gerber files, and BOM) are located in the `/KiCad` directory of this repository.

* **`/gerber`**: Manufacturing files for the PCB.
* **`/schematic`**: Schematic files (`.sch`) and PDF export.
* **`/pcb`**: PCB layout files (`.brd`, `.kicad_pcb`, etc.)

