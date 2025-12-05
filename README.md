# 🖊️ DIY Arduino CNC Plotter (28BYJ-48 + Servo)

A low-cost, open-source desktop CNC plotter (drawing robot) powered by an Arduino Uno. This project is designed to create precise drawings using affordable 28BYJ-48 stepper motors and a servo motor for the Z-axis (pen lift mechanism).

![Project Status](https://img.shields.io/badge/Status-Completed-success)
![Hardware](https://img.shields.io/badge/Hardware-Arduino_Uno-blue)
![License](https://img.shields.io/badge/License-MIT-green)

## 📋 Features
* **Budget-Friendly:** Built using inexpensive components available worldwide.
* **Servo Z-Axis:** Utilizes a standard SG90 servo for lifting and lowering the pen, replacing heavy Z-axis mechanisms.
* **Custom Firmware:** Runs on a modified version of GRBL specifically tuned for 28BYJ-48 steppers and servo control.
* **3D Printable:** All mechanical parts are designed for 3D printing (STL files included).

---

## 🛠️ Hardware Requirements (BOM)

### Electronics:
* [1x] **Arduino Uno** (with USB cable)
* [2x] **28BYJ-48 Stepper Motors** (5V)
* [2x] **ULN2003 Stepper Drivers**
* [1x] **Micro Servo** (SG90 or equivalent)
* [1x] **Micro USB Breakout Board** (Female) - for external power (optional but recommended)
* Jumper wires (Male-to-Female, Male-to-Male)

### Mechanics:
* [6x] 5mm Smooth Rods (Steel shafts)
* [4x] GT2 Timing Pulleys (20 Teeth)
* [2x] GT2 Timing Belt (~1 meter each)
* [1x] Pen, marker, or pencil
* M3 Screws and nuts for assembly

---

## 📂 Repository Structure

* `/Firmware` — Modified GRBL source code supporting the servo Z-axis.
* `/3D_Models` — Contains `CNC Plotter 3D Models.stl` with all printable parts.
* `/Schematics` — Wiring diagrams:
    * `CNC Plotter.fzz` (Fritzing source file)
    * `Circuit Diagram.png` (Visual reference)
* `/Software` — Links to necessary PC software (Inkscape, extensions, etc.).

---

## 🔌 Wiring & Connection

Please refer to `Circuit Diagram.png` in the `/Schematics` folder for the visual guide.

**Pinout Summary:**
* **X-Axis (Stepper 1):** Arduino Pins `2, 3, 4, 5` → ULN2003 Driver IN1, IN2, IN3, IN4
* **Y-Axis (Stepper 2):** Arduino Pins `6, 7, 8, 9` → ULN2003 Driver IN1, IN2, IN3, IN4
* **Z-Axis (Servo):** Arduino Pin `11` (Signal), `5V`, `GND`
* **Power:** Do not power both motors directly from the Arduino 5V pin. Use an external 5V power supply connected to the drivers.

---

## 💻 Software Prerequisites

To use this plotter, you will need the following tools:

1.  **Firmware:**
    * Upload the code found in the `/Firmware` folder to your Arduino Uno using the Arduino IDE.
    * *Note:* Standard GRBL **will not work** as it does not support servo motors for the Z-axis.

2.  **G-Code Generation (Inkscape):**
    * **Inkscape:** Vector graphics editor.
    * **MI Inkscape Extension:** A plugin to generate G-Code that uses `M3` and `M5` commands for the servo pen lift.

3.  **G-Code Sender:**
    * **Universal G-Code Sender (UGS):** Platform to send the G-Code file to the Arduino.

---

## 🚀 How to Run

1.  **Print:** 3D print all components found in `/3D_Models`.
2.  **Assemble:** Construct the frame using the rods and screws. Mount the motors.
3.  **Wire:** Connect the electronics according to the scheme in `/Schematics`.
4.  **Flash:** Open the project in the `/Firmware` folder and upload it to your Arduino Uno.
5.  **Connect:** Open **Universal G-Code Sender**, select the correct COM port and set the baud rate (usually `115200`).
6.  **Plot:** Load your G-Code file and click "Send".

---

## ⚙️ GRBL Configuration Tips

After flashing, you may need to calibrate the steps per mm in the GRBL console (via UGS) to ensure accurate sizing.
Typical settings for 28BYJ-48 motors:

```text
$100=... (X-axis steps/mm)
$101=... (Y-axis steps/mm)
