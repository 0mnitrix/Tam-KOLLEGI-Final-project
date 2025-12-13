
#  Low-Cost DIY CNC Pen Plotter 

A budget-friendly 2-axis CNC drawing machine based on **Arduino Uno** and **GRBL**. Designed to create precise vector drawings using affordable 28BYJ-48 stepper motors and a servo motor for the pen lift mechanism.

> **Key Feature:** This repository contains a **custom-patched version of the GRBL library** inside the `Firmware/` folder, specifically adapted to run on **Windows 11**, fixing compatibility issues with modern Arduino IDEs.


---

##  Features
* **Budget-Friendly:** Built using inexpensive components (28BYJ-48 steppers).
* **Servo Z-Axis:** Uses a standard SG90 servo for lifting the pen (commands M3/M5).
* **Windows 11 Ready:** Includes a patched `print.c` configuration for modern OS support.
* **Vibration Dampening:** Custom engineering solution to reduce pen wobble.

---

##  Hardware Requirements (BOM)

### Electronics:
* [1x] **Arduino Uno** (with USB cable)
* [2x] **28BYJ-48 Stepper Motors** (5V) + **ULN2003 Drivers**
* [1x] **Micro Servo** (SG90) for Z-axis
* [1x] **External 5V / 2A Power Supply** (Crucial for stability)
* Jumper wires (Male-to-Female, Male-to-Male)

### Mechanics:
* [6x] 5mm Smooth Rods (Steel shafts)
* [4x] GT2 Timing Pulleys (20 Teeth)
* [2x] GT2 Timing Belt (~1 meter each)
* Custom 3D-printed chassis parts (PLA)

---

##  Wiring & Pinout

Connect the motors to the Arduino as follows. **Do not power motors directly from Arduino 5V!** Use an external power supply.

| Component | Arduino Pin | Driver Pin |
| :--- | :--- | :--- |
| **X-Axis Motor** | Digital **2, 3, 4, 5** | ULN2003 IN1, IN2, IN3, IN4 |
| **Y-Axis Motor** | Digital **6, 7, 8, 9** | ULN2003 IN1, IN2, IN3, IN4 |
| **Z-Axis (Servo)** | Digital **11** | Signal (Orange/Yellow wire) |
| **Power** | GND | Connect Power Supply GND to Arduino GND |

Please refer to the diagrams in the `Schematics/` folder for visual guides.

---

##  Software & Installation

### 1. Arduino Firmware (The Windows 11 Fix)
Standard GRBL libraries often fail on Windows 11. Use our patched version found in this repo:

1.  **Clone this repo:**
    ```bash
    git clone [https://github.com/0mnitrix/Tam-KOLLEGI-Final-project.git](https://github.com/0mnitrix/Tam-KOLLEGI-Final-project.git)
    ```
2.  **Install Library:**
    * Go to the `Firmware/` folder.
    * Copy the GRBL library folder to your local Arduino libraries path (usually `Documents/Arduino/libraries`).
    * *Warning:* Delete any existing "GRBL" libraries to avoid conflicts.
3.  **Flash:**
    * Open the sketch inside `Firmware/` using Arduino IDE.
    * Upload to your board.

### 2. G-Code Generation
* **Inkscape:** Use for creating vector graphics.
* **Extension:** Check the `Software/` folder for the **MI Inkscape Extension** or links to download it. This plugin correctly handles `M3` (Pen Down) and `M5` (Pen Up) commands.

### 3. Sending Code
* **Universal G-Code Sender (UGS):** Recommended platform.
    * Baud Rate: `115200`

---

##  Repository Structure

```text
├── 3D_Models/       # STL files for 3D printing the chassis
├── Firmware/        # Patched GRBL Library & Upload Sketch
├── Photos/          # Project gallery and assembly photos
├── Schematics/      # Wiring diagrams and Fritzing files
├── Software/        # Tools and extensions (Inkscape plugins)
└── README.md        # This file
````

-----

##  Future Improvements

  - [ ] **Expanded Area:** Scale the frame to support **A4 size** (21x29.7cm).
  - [ ] **NEMA 17 Upgrade:** Replace 28BYJ-48s with NEMA 17 motors for 500% faster plotting speed.
  - [ ] **Custom PCB:** Replace jumper wires with a soldered shield for reliability.
