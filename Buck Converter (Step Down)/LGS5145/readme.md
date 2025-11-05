# LGS5145 55V, 1.0A Step-Down Converter PCB

This repository contains the hardware design files for a compact, high-efficiency DC-DC step-down (buck) converter based on the LGS5145 integrated circuit.

This PCB is designed to take a wide input voltage (4.5V to 55V) and convert it to a stable, lower output voltage with a continuous current capacity of up to 1.0A. The 1.2MHz switching frequency allows for the use of small, low-profile external components. Its wide input range makes it suitable for demanding applications, including 42V automotive power systems.

## Key Features

* **Wide Input Voltage Range:** 4.5V to 55V
* **Continuous Output Current:** 1.0A
* **High Efficiency:** Up to 90%, with high light-load efficiency via **SKIP Mode**.
* **High Switching Frequency:** 1.2MHz fixed frequency minimizes inductor and capacitor size.
* **Low Quiescent Current:** Approximately 150µA typical static operating current.
* **Internal Compensation:** Reduces external component count and design complexity.
* **Internal Protections:** Includes Cycle-by-Cycle Over Current Protection (OCP), Output Short Circuit Protection (Frequency Foldback), and Thermal Shutdown (TSD).
* **Compact Footprint:** Based on the SOT23-6 package.

## Technical Specifications

| Parameter | Value | Notes |
| :--- | :--- | :--- |
| **Integrated Circuit** | LGS5145 | |
| **Input Voltage (Vin)** | 4.5V – 55V |
| **Output Voltage (Vout)** | Configurable | Set by feedback resistors RF/RG. |
| **Max Output Current** | 1.0A | 1.2A Peak SW Current Limit |
| **Switching Frequency** | 1.2MHz | Fixed (PWM Operation) |
| **Feedback Voltage (Vref)** | 0.812V (Typical) | |
| **Quiescent Current** | \~150µA | (Typical, non-switching) |
| **Topology** | Asynchronous Buck | Requires an external Schottky diode. |
| **Protections** | OCP, TSD, SCP | |

## Connections and Pinout

* **VIN+**: Positive input voltage (4.5V to 55V)
* **GND**: Common ground for input and output
* **VOUT+**: Regulated positive output voltage
* **VOUT-**: Common ground for input and output


## Output Voltage Configuration

The output voltage (Vout) is set by the resistive divider formed by RF (top resistor) and RG (bottom resistor), connecting VOUT to the FB (Feedback) pin. The LGS5145 regulates the FB pin to a reference voltage (Vref) of **0.812V**.

The output voltage is calculated using the following formula:

$$
V_{out} = 0.812V \times (1 + \frac{RF}{RG})
$$

To calculate the resistor values for a desired output voltage (datasheet recommends RG ≤ 30kΩ):

$$
RF = RG \times (\frac{V_{out}}{0.812V} - 1)
$$

**Example:** For a 5V output, using the datasheet's recommended RG value of 16kΩ:

* `RF = 16kΩ * (5.0V / 0.812V - 1)`
* `RF = 16kΩ * (6.1576 - 1)`
* `RF = 16kΩ * 5.1576`
* `RF = 82.52kΩ`
* Use the nearest standard 1% resistor value: **82kΩ**. This will produce an output of `0.812V * (1 + 82k/16k) = 4.9735V`, which is well within a 1% tolerance.

### Common Voltage Settings

Here are suggested 1% standard resistor values for common output voltages.

| Target Vout | RF (Top Resistor) | RG (Bottom Resistor) | Calculated Vout |
| :--- | :--- | :--- | :--- |
| 1.8V | 24.3kΩ | 20kΩ | 1.800V |
| 2.5V | 6.8kΩ | 3.3kΩ | 2.485V |
| 3.3V | 30.9kΩ | 10kΩ | 3.321V |
| 5.0V | 82kΩ | 16kΩ | 4.974V |
| 9.0V | 182kΩ | 18kΩ | 9.020V |
| 12.0V | 300kΩ | 22kΩ | 11.884V |

---

## Schematic

<img width="954" height="313" alt="image" src="https://github.com/user-attachments/assets/21b3596e-5b93-487b-8a03-98822cd14952" />

## PCB 

![pcb](https://github.com/user-attachments/assets/1a3437f3-0be1-4180-8ac9-7bb9ca2cf496)


## Bill of Materials (BOM)

The component values below are typical. The inductor (L1) and output capacitor (C_out) values should be selected according to the LGS5145 datasheet guidelines for your specific Vout and Iout requirements.

| Reference | Component | Footprint | Notes |
| :--- | :--- | :--- | :--- |
| U1 | LGS5145 | SOT23-6 | |
| D1 | Schottky Diode | `[e.g., SOD-123]` | e.g., SS14. Must be rated for >Vin (max) and >Iout (max). |
| L1 | Inductor | `[e.g., 1210]` | e.g., 4.7µH - 10µH. Must have a saturation current > 1.2A. |
| C_in | Input Capacitor | `[e.g., 1206]` | e.g., 10µF, 100V X7R Ceramic. Place close to VIN and GND. |
| C_out | Output Capacitor | `[e.g., 1206]` | e.g., 22µF, 25V X7R Ceramic. |
| C_bst | Bootstrap Cap | `[e.g., 0603]` | **100nF**. Connect between BST (Pin 1) and SW (Pin 6). |
| RF | Feedback Resistor | `[e.g., 0603]` | Sets Vout (Top resistor). See "Output Voltage Configuration". |
| RG | Feedback Resistor | `[e.g., 0603]` | Sets Vout (Bottom resistor). e.g., 16kΩ. |
| `[C_ff]` | (Optional) | `[e.g., 0603]` | Feed-forward capacitor (e.g., 47pF) in parallel with RF. |
+ 2 * KF301-5.0-2P Connectors 

## Design Files

This project was designed using `[KiCad]`.

All original design files (schematic, PCB layout, Gerber files, and BOM) are located in the `/KiCad` directory of this repository.





* **CERN-OHL-S v2** (Strongly Reciprocal)
* **TAPR Open Hardware License**
* **MIT License** (Permissive, common for software but also used for simple hardware)
