# Job Card 1: Power & Vitals Engineer

**Role:** Power Distribution & System Monitor  
**Objective:** Design a stable power delivery network and a "System Controller" to monitor board health.

---

## 1. Functional Requirements
* **Input Power:** Accept **12V DC** from a standard wall adapter (Barrel Jack).
* **Primary Rail (5V):** Step down 12V $\rightarrow$ 5V to power the FPGA Core Board.
    * *Spec:* Must provide at least **3.0 Amps** continuous current.
    * *Ripple:* Low ripple (<30mV) is preferred for system stability.
* **Secondary Rail (3.3V):** Step down 5V $\rightarrow$ 3.3V for Peripherals (Ethernet, MCU, SD Card).
    * *Spec:* Must provide at least **1.0 Amp**.
* **System Controller:** Implement a Microcontroller (MCU) to:
    1.  Monitor Input Current (Amps) & Voltage.
    2.  Control a Cooling Fan based on temperature or load.
    3.  Act as a **USB-to-UART Bridge** for the FPGA Linux Console.
  (for a start, I would recommend a simple MCU like the ATMega. Make sure to include JTAG for programming)!

## 2. Constraints & Rules
* **Voltage Levels:** The FPGA Core Board requires exactly **5.0V** at its input pins. Do not exceed 5.2V.
* **Common Ground:** All grounds (12V, 5V, 3.3V, Signal GND) must be tied to a single continuous Ground Plane.
* **Logic Levels:** The MCU UART lines connecting to the FPGA must use **3.3V Logic**. (Do not use 5V logic).

## 3. Interfaces Needed
* **I2C:** Between MCU and Current Sensor.
* **UART:** Between MCU and FPGA (Bank 34/35).
* **PWM:** From MCU to Fan Transistor.

## 4. Breadboard Strategy
* **Feasibility:** High.
* **Task:** Build the full power regulation and MCU circuit on a breadboard. Use breakout modules for the regulators. Verify the 5V rail is stable under load *before* connecting the expensive FPGA.
